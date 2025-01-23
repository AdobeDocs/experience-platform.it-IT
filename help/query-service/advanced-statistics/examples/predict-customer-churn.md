---
title: Prevedere l'abbandono dei clienti con la regressione logistica basata su SQL
description: Scopri come prevedere l’abbandono dei clienti utilizzando la regressione logistica basata su SQL. Questa guida tratta l’intero processo, dalla creazione di modelli alla valutazione e previsione. Ottieni informazioni fruibili dal comportamento di acquisto dei clienti per implementare strategie di conservazione proattive e ottimizzare le decisioni aziendali.
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# Prevedere l&#39;abbandono dei clienti con la regressione logistica basata su SQL

Prevedere l’abbandono dei clienti aiuta le aziende a fidelizzare i clienti, ottimizzare le risorse e aumentare la redditività migliorando la soddisfazione e la fedeltà tramite informazioni fruibili.

Scopri come utilizzare la regressione logistica basata su SQL per prevedere l’abbandono dei clienti. Utilizza questa guida SQL completa per trasformare i dati grezzi di e-commerce in informazioni significative sul cliente in base a metriche comportamentali chiave (come frequenza di acquisto, valore medio dell’ordine e data di aggiornamento dell’ultimo acquisto). Il documento tratta l’intero processo, dalla preparazione dei dati e l’ingegneria delle funzioni, alla creazione di modelli, alla valutazione e alla previsione.

Utilizzare questa guida per creare un potente modello di previsione dell&#39;abbandono che identifichi i clienti a rischio, ottimizzi le strategie di conservazione e migliori decisioni aziendali. Include istruzioni dettagliate, query SQL e spiegazioni dettagliate per aiutarti ad applicare le tecniche di apprendimento automatico all’interno dell’ambiente di dati.

## Introduzione

Prima di creare il modello di abbandono, è importante esplorare le funzioni chiave del cliente e i requisiti dei dati. Le sezioni seguenti descrivono gli attributi essenziali del cliente e i campi di dati richiesti per una formazione accurata sui modelli.

### Definire le funzioni del cliente {#define-customer-features}

Per classificare con precisione l’abbandono, il modello analizza le abitudini e le tendenze di acquisto. La tabella seguente illustra le principali funzioni di comportamento dei clienti utilizzate nel modello:

| Funzione | Descrizione |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Numero totale di acquisti effettuati dal cliente. |
| `total_revenue` | Il totale dei ricavi generati dagli acquisti dei clienti. |
| `avg_order_value` | Il valore medio degli acquisti di un cliente. |
| `customer_lifetime` | Il numero di giorni tra il primo e l’ultimo acquisto del cliente. |
| `days_since_last_purchase` | Il numero di giorni dall’ultimo acquisto del cliente. |
| `purchase_frequency` | Il numero di mesi distinti in cui il cliente ha effettuato gli acquisti. |

### Ipotesi e campi obbligatori {#assumptions-required-fields}

Per generare previsioni di abbandono dei clienti, il modello dipende dai campi chiave della tabella `webevents` che acquisiscono i dettagli delle transazioni dei clienti. Il set di dati deve includere i campi seguenti:

| Campo | Descrizione |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Identificatore univoco utilizzato per tenere traccia dei clienti tra sessioni diverse. |
| `productListItems.priceTotal[0]` | Il costo totale degli articoli acquistati per transazione. |
| `productListItems.quantity[0]` | Numero totale di articoli in un acquisto. |
| `timestamp` | La data e l’ora esatte di ogni evento di acquisto. |
| `commerce.order.purchaseID` | Valore obbligatorio che conferma un acquisto completato. |

Il set di dati deve contenere record cronologici strutturati delle transazioni dei clienti, con ogni riga che rappresenta un evento di acquisto. Ogni evento deve includere marche temporali in un formato data-ora appropriato compatibile con la funzione SQL `DATEDIFF` (ad esempio, YYYY-MM-DD HH:MI:SS). Inoltre, ogni record deve contenere un ID Experience Cloud (`ECID`) valido nel campo `identityMap` per identificare in modo univoco i clienti.

>[!TIP]
>
>L’elaborazione di set di dati di grandi dimensioni con milioni di record può influire in modo significativo sulle prestazioni. Per ottimizzare l’esecuzione delle query, partiziona il set di dati di esperienza per marca temporale, esegui l’elaborazione incrementale utilizzando gli snapshot e applica funzioni di aggregazione efficienti in base alle esigenze. Inoltre, filtra i dati prima dell’aggregazione per ridurre il sovraccarico di elaborazione.

## Creare un modello {#create-a-model}

Per prevedere l’abbandono dei clienti, devi creare un modello di regressione logistica basato su SQL che analizza la cronologia degli acquisti dei clienti e le metriche comportamentali. Il modello classifica i clienti come `churned` o `not churned` determinando se hanno effettuato un acquisto negli ultimi 90 giorni.

### Usa SQL per creare il modello di previsione dell’abbandono {#sql-create-model}

Il modello basato su SQL elabora i dati `webevents` aggregando metriche chiave e assegnando etichette di abbandono in base a una regola di inattività di 90 giorni. Questo approccio distingue i clienti attivi dai clienti a rischio. La query SQL esegue inoltre la progettazione delle funzionalità per migliorare la precisione del modello e la classificazione dell&#39;abbandono. Queste informazioni consentono all&#39;azienda di implementare strategie di conservazione mirate, ridurre l&#39;abbandono e ottimizzare il valore del ciclo di vita del cliente.

>[!NOTE]
>
>Il modello di previsione dell’abbandono utilizza una soglia predefinita di 90 giorni per classificare i clienti come abbandonati. Per modificare questa soglia in modo da allinearla agli obiettivi aziendali e alle strategie di conservazione, modificare la condizione `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` nelle query SQL.

Utilizzare l&#39;istruzione SQL seguente per creare il modello `retention_model_logistic_reg` con le caratteristiche e le etichette specificate:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Output modello {#model-output}

Il set di dati di output contiene metriche relative al cliente e il relativo stato di abbandono. Ogni riga rappresenta un cliente, i relativi valori delle funzioni e lo stato di abbandono. Puoi utilizzare questo output per analizzare il comportamento dei clienti, addestrare modelli predittivi e sviluppare strategie di conservazione mirate per mantenere i clienti a rischio. Di seguito è riportato un esempio di tabella di output:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Colonna | Descrizione |
|-----------|------------------------------------------------------------------------------------|
| `churned` | Il valore indica se il cliente ha effettuato un acquisto negli ultimi 90 giorni (0 = non abbandonata, 1 = abbandonata). |

## Usa SQL per valutare il modello {#model-evaluation}

Quindi, valuta il modello di previsione dell’abbandono per determinarne l’efficacia nell’identificazione dei clienti a rischio. Valuta le prestazioni del modello con metriche chiave che misurano accuratezza e affidabilità.

Per misurare la precisione del modello `retention_model_logistic_reg` nella previsione dell&#39;abbandono dei clienti, utilizzare la funzione `model_evaluate`. L’esempio SQL seguente valuta il modello utilizzando un set di dati strutturato come i dati di apprendimento:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Output di valutazione modello

L’output di valutazione include metriche delle prestazioni chiave, come AUC-ROC, precisione e richiamo. Queste metriche forniscono informazioni sull’efficacia dei modelli, utili per perfezionare le strategie di conservazione e prendere decisioni basate sui dati.

>[!NOTE]
>
>I valori delle prestazioni variano da 0 a 1, dove 1,0 rappresenta le prestazioni perfette.

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Metrica | Descrizione |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Questa metrica indica la capacità del modello di distinguere tra clienti abbandonati e non abbandonati. Un valore più vicino a 1 indica prestazioni migliori. |
| `accuracy` | La metrica di accuratezza rappresenta la proporzione di previsioni corrette, fornendo una misura complessiva delle prestazioni del modello. |
| `precision` | Precision mostra la proporzione di clienti abbandonati correttamente identificati e indica l’affidabilità nella previsione di abbandono. Un valore elevato indica un numero inferiore di falsi positivi. |
| `recall` | Il richiamo misura la capacità del modello di identificare tutti i clienti abbandonati. Un valore di richiamo elevato indica un minor numero di clienti di abbandono. |

>[!NOTE]
>
>I punteggi quasi perfetti in questo esempio sono a scopo dimostrativo. In pratica, i dati reali possono produrre valori più bassi a causa del rumore e della variabilità.

## Previsione del modello {#model-prediction}

Una volta valutato il modello, utilizzare `model_predict` per applicarlo a un nuovo set di dati e prevedere l&#39;abbandono dei clienti. È possibile utilizzare queste previsioni per identificare i clienti a rischio e implementare strategie di conservazione mirate.

### Usa SQL per generare previsioni di abbandono {#sql-model-predict}

La query SQL seguente utilizza il modello `retention_model_logistic_reg` per prevedere l&#39;abbandono dei clienti con un set di dati strutturato come i dati di formazione:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Output di previsione del modello {#prediction-output}

Il set di dati di output include le funzioni chiave del cliente e lo stato di abbandono previsto, che indica se è probabile che un cliente abbandoni. Utilizza queste informazioni per implementare strategie di conservazione proattive e ridurre l’abbandono dei clienti.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Colonna | Descrizione |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | Lo stato di abbandono previsto del cliente in base al modello (0 = non abbandonati, 1 = abbandonati). |

## Passaggi successivi

Ora hai imparato a creare, valutare e utilizzare un modello basato su SQL per prevedere l’abbandono dei clienti. Con questa base, è possibile analizzare il comportamento dei clienti, identificare i clienti a rischio e implementare strategie di conservazione proattiva per migliorare la customer retention. Per migliorare ulteriormente e applicare il modello di previsione dell’abbandono, considera i seguenti passaggi:

- Automatizzare il processo: integra il modello in una pipeline di dati per un monitoraggio continuo e informazioni in tempo reale. [Scopri come verificare ed elaborare i set di dati con SQL](../../../dashboards/query.md).
- Monitora le prestazioni del modello: valuta continuamente il modello con nuovi dati per mantenere accuratezza e rilevanza.  Utilizza [Assistente AI](../../../ai-assistant/landing.md) nell&#39;interfaccia utente di Adobe Experience Platform per monitorare le modifiche delle prestazioni chiave e [prevedere le tendenze del pubblico](../../../ai-assistant/new-features/audience-forecasting.md).
