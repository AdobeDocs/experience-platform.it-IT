---
title: Modelli
description: Modellare la gestione del ciclo di vita con l'estensione Data Distiller SQL. Scopri come creare, addestrare e gestire modelli statistici avanzati utilizzando SQL, inclusi processi chiave come il controllo delle versioni, la valutazione e la previsione dei modelli, per ricavare informazioni fruibili dai tuoi dati.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 1%

---

# Modelli

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Query Service ora supporta i processi principali di creazione e distribuzione di un modello. È possibile utilizzare SQL per addestrare il modello utilizzando i dati, valutarne la precisione e quindi utilizzare il modello addestrato per effettuare previsioni sui nuovi dati. Puoi quindi utilizzare il modello per generalizzare dai dati passati per prendere decisioni informate su scenari reali.

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

>[!TIP]
>
>Per un riferimento completo alla clausola `TRANSFORM`, incluse le funzioni e l&#39;utilizzo supportati in `CREATE MODEL` e `CREATE TABLE`, vedere la clausola [`TRANSFORM` nella documentazione relativa alla sintassi SQL](../sql/syntax.md#transform).

## Aggiornare un modello {#update}

Scopri come aggiornare un modello di apprendimento automatico esistente applicando nuove trasformazioni di ingegneria delle funzioni e configurando opzioni quali il tipo di algoritmo e la colonna delle etichette. Ogni aggiornamento crea una nuova versione del modello, incrementata rispetto all&#39;ultima versione. In questo modo è possibile tenere traccia delle modifiche e riutilizzare il modello in fasi di valutazione o previsione future.

L&#39;esempio seguente illustra come aggiornare un modello con nuove trasformazioni e opzioni:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Esempio**

Per comprendere meglio il processo di controllo delle versioni, prendere in considerazione il comando seguente:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Dopo l&#39;esecuzione di questo comando, il modello presenta una nuova versione, come illustrato nella tabella seguente:

| ID modello aggiornato | Modello aggiornato | Nuova versione |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

Le note seguenti spiegano i componenti e le opzioni chiave nel flusso di lavoro di aggiornamento del modello.

- `UPDATE model <model_alias>`: il comando update gestisce il controllo delle versioni e crea una nuova versione del modello incrementata rispetto all&#39;ultima versione.
- `version`: parola chiave facoltativa utilizzata solo durante gli aggiornamenti per specificare in modo esplicito che deve essere creata una nuova versione. Se omesso, il sistema incrementa automaticamente la versione.

### Visualizzare in anteprima e rendere persistenti le feature trasformate {#preview-transform-output}

Utilizzare la clausola `TRANSFORM` nelle istruzioni `CREATE TABLE` e `CREATE TEMP TABLE` per visualizzare in anteprima e mantenere l&#39;output delle trasformazioni delle funzionalità prima dell&#39;apprendimento del modello. Questo miglioramento fornisce visibilità sul modo in cui le funzioni di trasformazione (come la codifica, la tokenizzazione e l’assemblatore vettoriale) vengono applicate al set di dati.

Materializzando i dati trasformati in una tabella autonoma, è possibile esaminare le feature intermedie, convalidare la logica di elaborazione e garantire la qualità delle feature prima di creare un modello. Ciò migliora la trasparenza nell’intera pipeline di apprendimento automatico e supporta un processo decisionale più informato durante lo sviluppo di modelli.

#### Sintassi {#syntax}

Utilizzare la clausola `TRANSFORM` in un&#39;istruzione `CREATE TABLE` o `CREATE TEMP TABLE` come illustrato di seguito:

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

Oppure:

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Esempio**

Creare una tabella utilizzando le trasformazioni di base:

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Creare una tabella temporanea utilizzando i passi di ingegneria delle feature aggiuntivi riportati di seguito.

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

Quindi esegui una query sull’output:

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Considerazioni importanti {#considerations}

Questa funzionalità migliora la trasparenza e supporta la convalida della funzionalità, ma presenta alcune limitazioni importanti da considerare quando si utilizza la clausola `TRANSFORM` al di fuori della creazione del modello.

- **Output vettoriali**: se la trasformazione genera output di tipo vettoriale, questi vengono automaticamente convertiti in array.
- **Limitazione del riutilizzo dei batch**: le tabelle create con `TRANSFORM` possono applicare trasformazioni solo durante la creazione della tabella. I nuovi batch di dati inseriti con `INSERT INTO` sono **non trasformati automaticamente**. Per applicare la stessa logica di trasformazione ai nuovi dati, è necessario ricreare la tabella utilizzando una nuova istruzione `CREATE TABLE AS SELECT` (CTAS).
- **Limitazione riutilizzo modello**: le tabelle create con `TRANSFORM` non possono essere utilizzate direttamente nelle istruzioni `CREATE MODEL`. Ridefinire la logica `TRANSFORM` durante la creazione del modello. Le trasformazioni che producono output di tipo vettoriale non sono supportate durante l&#39;apprendimento del modello. Per ulteriori informazioni, vedere [Tipi di dati di output della trasformazione delle funzionalità](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Questa funzione è progettata per l&#39;ispezione e la convalida. Non sostituisce la logica della pipeline riutilizzabile. Qualsiasi trasformazione destinata all&#39;input del modello deve essere esplicitamente ridefinita nel passaggio di creazione del modello.

## Valuta modelli {#evaluate-model}

Per garantire risultati affidabili, valutare la precisione e l&#39;efficacia del modello prima di distribuirlo per le previsioni con la parola chiave `model_evaluate`. L&#39;istruzione SQL seguente specifica un set di dati di test, colonne specifiche e la versione del modello per testare il modello valutandone le prestazioni.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

La funzione `model_evaluate` considera `model-alias` come primo argomento e un&#39;istruzione flessibile `SELECT` come secondo argomento. Query Service esegue innanzitutto l&#39;istruzione `SELECT` e mappa i risultati sulla funzione definita da Adobe (ADF) `model_evaluate`. Il sistema prevede che i nomi di colonna e i tipi di dati nel risultato dell&#39;istruzione `SELECT` corrispondano a quelli utilizzati nel passaggio di apprendimento. Questi nomi di colonna e tipi di dati vengono trattati come dati di prova e dati di etichetta per la valutazione.

>[!IMPORTANT]
>
>Durante la valutazione (`model_evaluate`) e la previsione (`model_predict`), vengono utilizzate le trasformazioni eseguite durante l&#39;addestramento.

## Previsione {#predict}

>[!IMPORTANT]
>
>La selezione avanzata delle colonne e l&#39;alias per `model_predict` sono controllati da un flag di funzionalità. Per impostazione predefinita, i campi intermedi come `probability` e `rawPrediction` non sono inclusi nell&#39;output di previsione.\
>Per abilitare l&#39;accesso a questi campi intermedi, eseguire il comando seguente prima di eseguire `model_predict`:
>
>`set advanced_statistics_show_hidden_fields=true;`

Utilizzare la parola chiave `model_predict` per applicare il modello e la versione specificati a un set di dati e generare previsioni. È possibile selezionare tutte le colonne di output, scegliere colonne specifiche o assegnare alias per migliorare la chiarezza dell&#39;output.

Per impostazione predefinita, vengono restituite solo le colonne di base e la previsione finale, a meno che il flag di funzione non sia abilitato.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Seleziona campi di output specifici {#select-specific-output-fields}

Quando il flag di funzione è abilitato, è possibile recuperare un sottoinsieme di campi dall&#39;output `model_predict`. Utilizzare questa opzione per recuperare i risultati intermedi, ad esempio le probabilità di previsione, i punteggi di previsione non elaborati e le colonne di base dalla query di input.

**Caso 1: restituire tutti i campi di output disponibili**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Scenario 2: restituire le colonne selezionate**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Caso 3: restituisce le colonne selezionate con alias**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

In ogni caso, l&#39;esterno `SELECT` controlla quali campi risultato vengono restituiti. Questi includono i campi base della query di input, insieme agli output di previsione come `probability`, `rawPrediction` e `predictionCol`.

### Mantenere le previsioni utilizzando CREATE TABLE o INSERT INTO

È possibile rendere persistenti le previsioni utilizzando &quot;CREATE TABLE AS SELECT&quot; o &quot;INSERT INTO SELECT&quot;, incluse le uscite di previsione, se necessario.

**Esempio: creare una tabella con tutti i campi di output delle previsioni**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Esempio: inserire i campi di output selezionati con alias**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Questo offre flessibilità per selezionare e mantenere solo i campi di output delle previsioni e le colonne di base rilevanti per l’analisi a valle o il reporting.

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
