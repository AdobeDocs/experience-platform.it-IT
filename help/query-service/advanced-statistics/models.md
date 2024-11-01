---
title: Modelli
description: Modellare la gestione del ciclo di vita con l'estensione Data Distiller SQL. Scopri come creare, addestrare e gestire modelli statistici avanzati utilizzando SQL, inclusi processi chiave come il controllo delle versioni, la valutazione e la previsione dei modelli, per ricavare informazioni fruibili dai tuoi dati.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# Modelli

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Query Service ora supporta i processi principali di creazione e distribuzione di un modello. È possibile utilizzare SQL per addestrare il modello utilizzando i dati, valutarne la precisione e quindi applicare il modello di addestramento per effettuare previsioni sui nuovi dati. Puoi quindi utilizzare il modello per generalizzare dai dati passati per prendere decisioni informate su scenari reali.

I tre passaggi del ciclo di vita del modello per generare informazioni fruibili sono:

1. **Formazione**: il modello apprende i modelli dal set di dati fornito. (crea o sostituisci modello)
2. **Test/valutazione**: le prestazioni del modello vengono valutate utilizzando un set di dati separato. (`model_evaluate`)
3. **Previsione**: il modello addestrato viene utilizzato per fare previsioni su dati nuovi e non visti.

Utilizzare l&#39;estensione SQL del modello, aggiunta alla grammatica SQL esistente, per gestire il ciclo di vita del modello in base alle esigenze aziendali. Questo documento descrive le istruzioni SQL necessarie per creare o sostituire un modello, addestrare, valutare, riaddestrare quando necessario e prevedere informazioni approfondite.

## Creazione di modelli e formazione {#create-and-train}

Scopri come definire, configurare e addestrare un modello di apprendimento automatico utilizzando i comandi SQL. L&#39;istruzione SQL seguente illustra come creare un modello, applicare trasformazioni di ingegneria delle funzionalità e avviare il processo di formazione per garantire che il modello sia configurato correttamente per un utilizzo futuro. I seguenti comandi SQL descrivono diverse opzioni per la creazione e la gestione dei modelli:

- **CREA MODELLO**: crea e addestra un nuovo modello in un set di dati specificato. Se esiste già un modello con lo stesso nome, questo comando restituisce un errore.
- **CREA MODELLO SE NON ESISTE**: crea e addestra un nuovo modello solo se nel set di dati specificato non esiste già un modello con lo stesso nome.
- **CREA O SOSTITUISCI MODELLO**: crea e addestra un modello, sostituendo l&#39;ultima versione di un modello esistente con lo stesso nome nel set di dati specificato.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Esempio**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Per comprendere meglio i componenti e le configurazioni chiave del processo di creazione e formazione del modello, le note seguenti spiegano lo scopo e la funzione di ciascun elemento nell’esempio SQL precedente.

- `<model_alias>`: l&#39;alias del modello è un nome riutilizzabile assegnato al modello, a cui è possibile fare riferimento in seguito. È necessario assegnare un nome al modello.
- `transform`: la clausola transform viene utilizzata per applicare le trasformazioni di ingegneria delle caratteristiche (ad esempio, codifica a caldo e indicizzazione di stringhe) al set di dati prima di addestrare il modello. L&#39;ultima clausola dell&#39;istruzione `TRANSFORM` deve essere un `vector_assembler` con un elenco di colonne che comporrebbero le funzionalità per l&#39;apprendimento dei modelli o un tipo derivato di `vector_assembler` (ad esempio `max_abs_scaler(feature)`, `standard_scaler(feature)` e così via). Solo le colonne menzionate nell&#39;ultima clausola verranno utilizzate per l&#39;apprendimento; tutte le altre colonne, anche se incluse nella query `SELECT`, verranno escluse.
- `label = <label-COLUMN>`: la colonna dell’etichetta nel set di dati di formazione che specifica il target o il risultato che il modello intende prevedere.
- `training-dataset`: questa sintassi seleziona i dati utilizzati per addestrare il modello.
- `type = 'LogisticRegression'`: questa sintassi specifica il tipo di algoritmo di apprendimento automatico da utilizzare. Le opzioni includono `LinearRegression`, `LogisticRegression` e `KMeans`.
- `options`: questa parola chiave fornisce un set flessibile di coppie chiave-valore per configurare il modello.
   - `Key model_type`: `model_type = '<supported algorithm>'`: specifica il tipo di algoritmo di apprendimento automatico da utilizzare. Le opzioni supportate sono `LinearRegression`, `LogisticRegression` e `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: definisce la colonna dell&#39;etichetta nel set di dati di apprendimento, che indica il target o il risultato che il modello intende prevedere.

Utilizza SQL per fare riferimento al set di dati utilizzato per l’apprendimento.

## Aggiornare un modello {#update}

Scopri come aggiornare un modello di apprendimento automatico esistente applicando nuove trasformazioni di ingegneria delle funzioni e configurando opzioni come il tipo di algoritmo e la colonna delle etichette. L&#39;istruzione SQL seguente illustra come aumentare il numero di versione del modello con ogni aggiornamento e garantire che le modifiche vengano tracciate in modo che il modello possa essere riutilizzato nei passaggi futuri di valutazione o previsione.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

Per comprendere come gestire le versioni dei modelli e applicare le trasformazioni in modo efficace, le note seguenti spiegano i componenti e le opzioni chiave nel flusso di lavoro di aggiornamento dei modelli.

- `UPDATE model <model_alias>`: il comando update gestisce il controllo delle versioni e aumenta il numero di versione del modello con ogni aggiornamento.
- `version`: parola chiave facoltativa utilizzata solo durante gli aggiornamenti per creare una nuova versione del modello.

## Valuta modelli {#evaluate-model}

Per garantire risultati affidabili, valutare la precisione e l&#39;efficacia del modello prima di distribuirlo per le previsioni con la parola chiave `model_evaluate`. L&#39;istruzione SQL seguente specifica un set di dati di test, colonne specifiche e la versione del modello per testare il modello valutandone le prestazioni.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

La funzione `model_evaluate` considera `model-alias` come primo argomento e un&#39;istruzione flessibile `SELECT` come secondo argomento. Query Service esegue innanzitutto l&#39;istruzione `SELECT` e associa i risultati alla funzione definita dall&#39;Adobe (ADF) `model_evaluate`. Il sistema prevede che i nomi di colonna e i tipi di dati nel risultato dell&#39;istruzione `SELECT` corrispondano a quelli utilizzati nel passaggio di apprendimento. Questi nomi di colonna e tipi di dati vengono trattati come dati di prova e dati di etichetta per la valutazione.

>[!IMPORTANT]
>
>Durante la valutazione (`model_evaluate`) e la previsione (`model_predict`), vengono utilizzate le trasformazioni eseguite durante l&#39;addestramento.

## Previsione {#predict}

Quindi, utilizza la parola chiave `model_predict` per applicare il modello e la versione specificati a un set di dati e generare previsioni per le colonne selezionate. L&#39;istruzione SQL seguente illustra questo processo, mostrando come prevedere i risultati utilizzando l&#39;alias e la versione del modello.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` accetta l&#39;alias del modello come primo argomento e un&#39;istruzione flessibile `SELECT` come secondo argomento. Query Service esegue innanzitutto l&#39;istruzione `SELECT` e mappa i risultati sull&#39;ADF `model_predict`. Il sistema prevede che i nomi di colonna e i tipi di dati nel risultato dell&#39;istruzione `SELECT` corrispondano a quelli del passaggio di apprendimento. Questi dati vengono quindi utilizzati per assegnare un punteggio e generare previsioni.

>[!IMPORTANT]
>
>Durante la valutazione (`model_evaluate`) e la previsione (`model_predict`), vengono utilizzate le trasformazioni eseguite durante l&#39;addestramento.

## Valutazione e gestione dei modelli

Utilizzare il comando `SHOW MODELS` per elencare tutti i modelli disponibili creati. Utilizzala per visualizzare i modelli che sono stati addestrati e sono disponibili per la valutazione o la previsione. Quando viene eseguita una query, le informazioni vengono recuperate dall’archivio modelli, che viene aggiornato durante la creazione del modello. I dettagli restituiti sono: ID modello, nome modello, versione, set di dati di origine, dettagli algoritmo, opzioni/parametri, ora di creazione/aggiornamento e l’utente che ha creato il modello.

```sql
SHOW MODELS;
```

I risultati vengono visualizzati in una tabella simile a quella riportata di seguito:

| model-id | model-name | version | set di dati sorgente | tipo | opzioni | trasformazione | campi | creato | aggiornato | creato DA |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 10:30 | 2024-08-14 11:00 | `JohnSnow@adobe.com` |

## Pulizia e manutenzione dei modelli

Utilizzare il comando `DROP MODELS` per eliminare i modelli creati dal registro dei modelli. Puoi utilizzarlo per rimuovere modelli obsoleti, inutilizzati o indesiderati. In questo modo si liberano risorse e si garantisce il mantenimento di solo modelli pertinenti. Per una maggiore specificità, potete anche includere un nome di modello facoltativo. Questo rilascia solo il modello con la versione del modello fornita.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Passaggi successivi

Dopo aver letto questo documento, è ora possibile comprendere la sintassi SQL di base necessaria per creare, addestrare e gestire modelli affidabili utilizzando Data Distiller. Quindi, esplora il documento [Implementare modelli statistici avanzati](./implement-models/implement-models.md) per scoprire i vari modelli attendibili disponibili e come implementarli in modo efficace nei flussi di lavoro SQL. Se non lo hai già fatto, assicurati di rivedere il documento [Ingegneria delle funzioni](./feature-engineering.md) per assicurarti che i tuoi dati siano preparati in modo ottimale per l&#39;apprendimento dei modelli.
