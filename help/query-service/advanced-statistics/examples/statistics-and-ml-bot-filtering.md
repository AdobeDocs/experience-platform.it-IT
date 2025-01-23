---
title: Filtraggio dei bot tramite statistiche e apprendimento automatico
description: Scopri come utilizzare le statistiche di Data Distiller e l’apprendimento automatico per identificare e filtrare le attività bot, in modo da garantire analisi accurate e una maggiore integrità dei dati.
source-git-commit: a8abbf61bdc646c0834c296a64b27c71c98ea1d3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Filtraggio dei bot tramite statistiche e apprendimento automatico

Le applicazioni pratiche del filtro dei bot interessano vari settori. Nell’e-commerce, migliora l’affidabilità delle metriche del tasso di conversione, i siti web di notizie possono beneficiare della riduzione delle metriche di coinvolgimento false e le reti pubblicitarie possono garantire una fatturazione equa. Per mantenere un’analisi accurata e garantire l’integrità dei dati nel traffico web o clickstream, devi indirizzare l’attività bot. Puoi garantire dati di analisi di alta qualità utilizzando Data Distiller per implementare un filtro bot efficace ed eliminare il traffico indesiderato.

Questo documento fornisce una guida completa per identificare e filtrare le attività bot utilizzando tecniche SQL e di machine learning. Presenta una progressione di approcci complementari, a partire dal filtraggio di base e dai progressi verso il rilevamento e la valutazione basati sull&#39;apprendimento automatico. Adottate questo solido framework per migliorare il rilevamento dei bot e mantenere l&#39;integrità dei dati.

## Comprendere l’attività bot {#understand-bot-activity}

L’attività dei bot può essere identificata rilevando picchi nelle azioni degli utenti entro intervalli di tempo specifici. Ad esempio, un numero eccessivo di clic eseguiti da un singolo utente in un breve arco di tempo potrebbe indicare un comportamento da bot. I due attributi chiave utilizzati nel filtro dei bot sono:

- **ECID (ID visitatore Experience Cloud):** un ID universale e costante che identifica i visitatori.
- **Timestamp:** l&#39;ora e la data in cui si verifica un&#39;attività sul sito Web.

Gli esempi seguenti mostrano come utilizzare le tecniche di SQL e machine learning per identificare, perfezionare e prevedere le attività bot. Utilizza questi metodi per migliorare l’integrità dei dati e garantire analisi utilizzabili.

## Filtraggio bot basato su SQL {#sql-based-bot-filtering}

Questo esempio di filtro bot basato su SQL illustra come utilizzare le query SQL per definire le soglie e rilevare l’attività bot in base a regole predefinite. Questo approccio fondamentale consente di identificare le anomalie nel traffico web rimuovendo le attività insolite. Personalizzando le regole di rilevamento con soglie e intervalli definiti, puoi personalizzare efficacemente il filtro dei bot in base a specifici pattern di traffico.

### Definire le soglie per l’attività bot {#define-thresholds}

Inizia analizzando il set di dati per identificare e classificare il comportamento degli utenti. Concentrati su attributi come ECID, timestamp e `webPageDetails.name` (il nome della pagina web visitata) per raggruppare le azioni degli utenti e rilevare i modelli che indicano l’attività di bot.

La query SQL seguente illustra come applicare la soglia di più di 60 clic in un minuto per identificare un’attività sospetta:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Espandi a intervalli multipli {#expand-to-multiple-intervals}

Quindi, definisci intervalli di tempo diversi per le soglie. Tali intervalli possono includere:

- **Intervallo di 1 minuto:** Fino a 60 clic.
- **Intervallo di 5 minuti:** Fino a 300 clic.
- **Intervallo di 30 minuti:** fino a 1800 clic.

La query SQL seguente crea una visualizzazione denominata `analytics_events_clicks_count_criteria` per gestire le soglie in più intervalli. L’istruzione consolida i conteggi dei clic per intervalli di 1 minuto, 5 minuti e 30 minuti in un set di dati strutturato e contrassegna le potenziali attività bot in base a soglie predefinite.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

L&#39;istruzione unisce i dati di `table_count_1_min`, `table_count_5_mins` e `table_count_30_mins` utilizzando il valore `mcid` e la pagina Web. Quindi consolida i conteggi dei clic per ogni utente su più intervalli di tempo per fornire una visualizzazione completa dell’attività dell’utente. Infine, la logica di segnalazione identifica gli utenti che superano i 50 clic in un minuto e li contrassegna come bot (`isBot = 1`).

### Struttura del set di dati di output

Il set di dati di output è strutturato con campi sia piatti che nidificati. Questa struttura offre flessibilità nel rilevare traffico anomalo e supporta strategie di filtro avanzate che utilizzano SQL e machine learning. I campi nidificati includono `count` e `web` che incapsulano dettagli granulari sulle soglie di attività e sulle pagine Web. L’acquisizione di queste metriche consente di estrarre facilmente le funzioni per attività di formazione e previsione.

Il diagramma di schema seguente illustra la struttura del set di dati risultante ed evidenzia come i campi nidificati e flat possono essere utilizzati per un’elaborazione efficiente e il rilevamento di bot.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### Set di dati di output da utilizzare per l’apprendimento

Il risultato di questa espressione potrebbe essere simile alla tabella fornita di seguito. Nella tabella, la colonna `isBot` funge da etichetta che distingue tra attività bot e non bot.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Funzioni statistiche avanzate per il filtro dei bot {#statistical-functions-for-bot-filtering}

Questo secondo esempio si basa sul filtro SQL di base incorporando tecniche di machine learning per perfezionare le soglie e migliorare l’accuratezza del filtro. Utilizzando funzioni statistiche avanzate, come l’analisi di regressione o gli algoritmi di clustering, questo approccio introduce funzionalità predittive utilizzabili per sviluppare modelli per la gestione di set di dati complessi con maggiore precisione.

### Creare un set di dati di formazione {#build-a-training-dataset}

In primo luogo, prepara un set di dati con strutture piane e nidificate utilizzabili dal modello di apprendimento automatico (come descritto in precedenza). Ulteriori indicazioni su come eseguire questa operazione sono disponibili nella [documentazione sull&#39;utilizzo di strutture di dati nidificate](../../key-concepts/nested-data-structures.md). Raggruppa i dati per marca temporale, ID utente e nome della pagina web per identificare i pattern nell’attività di bot.

### Utilizzare le clausole TRANSFORM e OPTIONS per la creazione di modelli {#transform-and-preprocess}

Per trasformare il set di dati e configurare in modo efficace il modello di apprendimento automatico, segui i passaggi seguenti. I passaggi descrivono come gestire i valori nulli, preparare le feature e definire i parametri del modello per ottenere prestazioni ottimali.

>[!TIP]
>
>Per ulteriori informazioni sull&#39;utilizzo delle trasformazioni e sulla preelaborazione dei dati, consulta la [documentazione sulle tecniche di trasformazione delle funzionalità](../feature-transformation.md).

1. Per riempire i valori Null nelle colonne numeriche, stringa e booleane, utilizzare rispettivamente le funzioni `numeric_imputer`, `string_imputer` e `boolean_imputer`. Questo passaggio garantisce che l’algoritmo di apprendimento automatico possa elaborare i dati senza errori.
2. Applicate le trasformazioni delle feature per preparare i dati per la modellazione. Applica `binarized`, `quantile_discretizer` o `string_indexer` per categorizzare o standardizzare le colonne. Quindi, inserire l&#39;output degli imputer (`numeric_imputer` e `string_imputer`) nei trasformatori successivi come `string_indexer` o `quantile_discretizer` per creare funzionalità significative.
3. Utilizzare la funzione `vector_assembler` per combinare le colonne trasformate in una singola colonna di funzionalità. Ridimensionare quindi le funzionalità utilizzando `min_max_scaler` per normalizzare i valori per migliorare le prestazioni del modello. Nota: nell&#39;esempio SQL, l&#39;ultima trasformazione menzionata nella clausola TRANSFORM diventa la colonna della feature utilizzata dal modello di apprendimento automatico.
4. Specificare il tipo di modello ed eventuali altri iperparametri nella clausola OPTIONS. `decision_tree_classifier` ad esempio è stato scelto qui perché si tratta di un problema di classificazione. Altri parametri come `max_depth` sono stati regolati (`MAX_DEPTH=4`) per ottimizzare il modello per ottenere prestazioni migliori.
5. Combinare le funzioni ed etichettare i dati di output. Utilizzare la clausola SELECT per specificare il set di dati per l&#39;apprendimento. Questa clausola deve includere sia le colonne delle funzionalità (`count_per_id`, `web`, `id`) che la colonna dell&#39;etichetta (`isBot`), che indica se è probabile che un&#39;azione sia un bot.

L’istruzione potrebbe essere simile all’esempio seguente.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Risultato**

Nei risultati visualizzati di seguito, il modello `bot_filtering_model` è stato creato con un ID, un nome e una versione univoci. Questo output funge da riferimento per il tracciamento e la gestione dei modelli. Utilizza questi riferimenti per identificare esattamente la configurazione e la versione necessarie per le previsioni o le valutazioni.

```console
           Created Model ID           |       Created Model       | Version
--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Valuta il modello addestrato {#evaluate-trained-model}

Dopo aver creato il modello, utilizzare il comando `MODEL_EVALUATE` per valutarne le prestazioni. Questo passaggio garantisce che il modello soddisfi i requisiti di precisione e prestazioni per il rilevamento delle attività da bot.

Utilizzare i seguenti argomenti nel comando SQL per valutare il modello:

1. Specificare il nome del modello (`bot_filtering_model`) per indicare il modello da valutare. Questo nome deve corrispondere a quello creato in precedenza con il comando `CREATE MODEL`.
2. Specificare la versione del modello (`1`) nel secondo argomento per specificare la versione del modello che si desidera valutare. Se esistono più versioni, viene utilizzata la versione corretta.
3. Includi il set di dati di valutazione per definire il set di dati per la valutazione. Verificare che il set di dati includa le stesse colonne di funzionalità (`count_per_id`, `web`, `id`) e la stessa colonna di etichetta (`isBot`) utilizzata durante l&#39;apprendimento.

>[!NOTE]
>
>Le trasformazioni applicate durante l’apprendimento dei modelli vengono applicate automaticamente durante la valutazione.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Risultato**

La risposta include metriche quali precisione, richiamo e AUC-ROC. I risultati confermano le prestazioni del modello.

>[!NOTE]
>
>I valori compresi nell&#39;intervallo 0-1 rappresentano proporzioni o probabilità, mentre 1,0 indica prestazioni perfette.

```console
auc_roc | accuracy | precision | recall
---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Metrica** | **Descrizione** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Questa metrica indica quanto efficacemente il modello può classificare bot e non bot. È ampiamente utilizzato per valutare i modelli di classificazione. |
| `accuracy` | Percentuale di previsioni corrette eseguite dal modello. |
| `precision` | La proporzione di previsioni di bot reali tra tutti i bot previsti. |
| `recall` | Percentuale di bot effettivi rilevati su tutti i bot effettivi. |

>[!TIP]
>
>Per l’utilizzo nelle sandbox di produzione, valuta la possibilità di valutare il modello sui set di dati di test per assicurarti che venga generalizzato in modo efficace.

### Prevedere l’attività dei bot {#predict-bot-activity}

Utilizzare il comando `MODEL_PREDICT` con il modello addestrato per identificare gli utenti (`id`) che sono bot. Segui i passaggi seguenti per generare previsioni per identificare l’attività bot:

1. Utilizzare il nome del modello (`bot_filtering_model`) nel primo argomento per specificare quale modello utilizzare per le previsioni.
2. Specificare la versione del modello (`1`) nel secondo argomento per assicurarsi che venga utilizzata la versione corretta del modello.
3. Per fornire i dati corretti per le previsioni, utilizzare un&#39;istruzione SELECT per specificare le colonne delle funzionalità (`count_per_id`, `web`, `id`). Non includere la colonna etichetta (`isBot`) perché il modello genererà previsioni per questo campo.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Risultato**

La risposta include previsioni per ogni utente (`id`) insieme a dettagli sull&#39;attività e sul risultato della classificazione del modello. Questo output consente un esame dettagliato del comportamento dell’utente e della classificazione dell’attività bot da parte del modello.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

La tabella seguente spiega ogni metrica:

| Nome colonna | Descrizione |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | L’identificatore univoco di ogni utente. |
| `count.one_minute` | I clic aggregati contano per intervalli di 1 minuto. |
| `count.five_minute` | I clic aggregati contano per intervalli di 5 minuti. |
| `count.thirty_minute` | I clic aggregati contano per intervalli di 30 minuti. |
| `web.webpagedetails.name` | Nome della pagina Web visitata. Fornisce il contesto per l’attività dell’utente. |
| `prediction` | La previsione del modello. Un risultato di `1.0` indica che l&#39;utente è contrassegnato come bot in base ai modelli di attività. |

## Gestione dei modelli {#manage-models}

Per gestire i modelli di apprendimento automatico, utilizza le parole chiave SQL elencate nella sezione seguente.

### Elencare i modelli disponibili {#list-available-models}

Gestire e rivedere in modo efficiente i modelli con il comando `SHOW MODELS;`. Questo comando elenca tutti i modelli di apprendimento automatico creati nell’area di lavoro corrente. L’output fornisce una panoramica dei modelli disponibili e ne include nomi, versioni e altri metadati.

```sql
SHOW MODELS;
```

### Elimina modelli {#delete-models}

Per liberare risorse e garantire che vengano mantenuti solo i modelli rilevanti, utilizzare il comando `DROP MODEL` per rimuovere i modelli obsoleti o non necessari. Questo comando elimina qualsiasi modello di apprendimento automatico specificato dopo le parole chiave. Nell&#39;esempio seguente, `bot_filtering_model` viene rimosso dal sistema.

```sql
DROP MODEL bot_filtering_model;
```

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a identificare e filtrare le attività bot utilizzando SQL e le tecniche di machine learning con i metodi di Data Distiller. Quindi, applica questi concetti ai set di dati e automatizza la riqualificazione dei modelli per un miglioramento continuo.
