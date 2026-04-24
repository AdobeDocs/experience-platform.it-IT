---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;sintassi SQL;sql;ctas;CTAS;Crea tabella come selezione
solution: Experience Platform
title: Sintassi SQL in Query Service
description: Questo documento descrive e spiega la sintassi SQL supportata da Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '4737'
ht-degree: 1%

---

# Sintassi SQL in Query Service

È possibile utilizzare SQL ANSI standard per istruzioni `SELECT` e altri comandi limitati in Adobe Experience Platform Query Service. Questo documento descrive la sintassi SQL supportata da [!DNL Query Service].

## QUERY SELECT {#select-queries}

La sintassi seguente definisce una query `SELECT` supportata da [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

La sezione schede riportata di seguito fornisce le opzioni disponibili per le parole chiave FROM, GROUP e WITH.

>[!BEGINTABS]

>[!TAB `from_item`]

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

>[!TAB `grouping_element`]

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

Nelle sottosezioni seguenti vengono fornite informazioni dettagliate sulle clausole aggiuntive che è possibile utilizzare nelle query, purché rispettino il formato descritto in precedenza.

### clausola SNAPSHOT

Questa clausola può essere utilizzata per leggere in modo incrementale i dati su una tabella basata sugli ID snapshot. Un ID snapshot è un indicatore di punto di controllo rappresentato da un numero di tipo Long applicato a una tabella del data lake ogni volta che vi vengono scritti dati. La clausola `SNAPSHOT` viene associata alla relazione di tabella utilizzata accanto a.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Esempio

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN 'HEAD' AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND 'TAIL';

SELECT * FROM (SELECT id FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id) C;

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

>[!NOTE]
>
>Quando si utilizza `HEAD` o `TAIL` in una clausola `SNAPSHOT`, è necessario racchiuderli tra apici (ad esempio, &#39;HEAD&#39;, &#39;TAIL&#39;). Se si utilizzano senza virgolette, si verifica un errore di sintassi.

Nella tabella seguente viene illustrato il significato di ogni opzione di sintassi all&#39;interno della clausola SNAPSHOT.

| Sintassi | Significato |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Legge i dati a partire dall&#39;ID snapshot specificato (esclusivo). |
| `AS OF end_snapshot_id` | Legge i dati così come si trovavano nell’ID snapshot specificato (incluso). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Legge i dati tra gli ID snapshot iniziale e finale specificati. È esclusivo di `start_snapshot_id` e include `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | Legge i dati dall&#39;inizio (prima del primo snapshot) all&#39;ID snapshot iniziale specificato (incluso). Si noti che questa opzione restituisce solo righe in `start_snapshot_id`. |
| `BETWEEN end_snapshot_id AND TAIL` | Legge i dati da subito dopo il `end_snapshot_id` specificato alla fine del set di dati (escluso l&#39;ID snapshot). Ciò significa che se `end_snapshot_id` è l&#39;ultimo snapshot nel set di dati, la query restituirà zero righe perché non sono presenti snapshot oltre l&#39;ultimo snapshot. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Legge i dati a partire dall&#39;ID snapshot specificato da `table_to_be_queried` e li unisce ai dati da `table_to_be_joined` come in `your_chosen_snapshot_id`. Il join si basa sugli ID corrispondenti delle colonne ID delle due tabelle unite in join. |

Una clausola `SNAPSHOT` funziona con un alias di tabella o tabella ma non sopra una sottoquery o vista. Una clausola `SNAPSHOT` funziona ovunque sia possibile applicare una query `SELECT` su una tabella.

È inoltre possibile utilizzare `HEAD` e `TAIL` come valori di offset speciali per le clausole snapshot. L&#39;utilizzo di `HEAD` fa riferimento a un offset prima del primo snapshot, mentre `TAIL` fa riferimento a un offset dopo l&#39;ultimo snapshot.

>[!NOTE]
>
>Se si esegue una query tra due ID snapshot, possono verificarsi i due scenari seguenti se lo snapshot iniziale è scaduto e il flag di comportamento di fallback facoltativo (`resolve_fallback_snapshot_on_failure`) è impostato:
>
>- Se è impostato il flag di comportamento di fallback facoltativo, Query Service sceglie lo snapshot disponibile più recente, lo imposta come snapshot iniziale e restituisce i dati tra lo snapshot disponibile più recente e lo snapshot finale specificato. Questi dati sono **inclusivi** della prima istantanea disponibile.

### clausola WHERE

Per impostazione predefinita, le corrispondenze prodotte da una clausola `WHERE` in una query `SELECT` fanno distinzione tra maiuscole e minuscole. Se si desidera che le corrispondenze non distinguano tra maiuscole e minuscole, è possibile utilizzare la parola chiave `ILIKE` anziché `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logica delle clausole LIKE e ILIKE è illustrata nella tabella seguente:

| Clausa | Operatore |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Esempio**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Questa query restituisce clienti con nomi che iniziano in &quot;A&quot; o &quot;a&quot;.

### ISCRIVITI

Una query `SELECT` che utilizza join ha la seguente sintassi:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT, E TRANNE

Le clausole `UNION`, `INTERSECT` e `EXCEPT` vengono utilizzate per combinare o escludere righe simili da due o più tabelle:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREA TABELLA COME SELEZIONATA {#create-table-as-select}

Utilizzare il comando `CREATE TABLE AS SELECT` per materializzare i risultati di una query `SELECT` in una nuova tabella. Questa funzione è utile per creare set di dati trasformati, eseguire aggregazioni o visualizzare in anteprima i dati generati dalle feature prima di utilizzarli in un modello.

Se sei pronto a addestrare un modello utilizzando funzionalità trasformate, consulta la [documentazione sui modelli](../advanced-statistics/models.md) per informazioni sull&#39;utilizzo di `CREATE MODEL` con la clausola `TRANSFORM`.

You can optionally include a `TRANSFORM` clause to apply one or more feature engineering functions directly within the CTAS statement. Use `TRANSFORM` to inspect the results of your transformation logic before model training.

This syntax applies to both permanent and temporary tables.

```sql
CREATE TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

```sql
CREATE TEMP TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

| Parametro | Descrizione |
| ----- | ----- |
| `schema` | The title of the XDM schema. Use this clause only if you wish to associate the new table with an existing XDM schema. |
| `rowvalidation` | (Optional) Enables row-level validation for each batch ingested into the dataset. Default is true. |
| `label` | (Optional) Use the value `PROFILE` to label the dataset as enabled for Profile ingestion. |
| `transform` | (Optional) Applies feature engineering transformations (such as string indexing, one-hot encoding, or TF-IDF) before materializing  the dataset. This clause is used for previewing transformed features. See [`TRANSFORM` clause documentation](#transform) for more details. |
| `select_query` | A standard `SELECT` statement that defines the dataset. See the [`SELECT` queries section](#select-queries) for more details. |

>[!NOTE]
>
>The `SELECT` statement must include an alias for aggregate functions such as `COUNT`, `SUM`, or `MIN`. You can provide the `SELECT` query with or without parentheses. This applies whether or not the `TRANSFORM` clause is used.

**Esempi**

A basic example using a `TRANSFORM`clause to preview a few engineered features:

```sql
CREATE TABLE ctas_transform_table_vp14 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review_e2e_DND;
```

A more advanced example with multiple transformation steps:

```sql
CREATE TABLE ctas_transform_table 
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

A temporary table example:

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

#### Limitations and behavior {#limitations-and-behavior}

Keep the following limitations in mind when using the `TRANSFORM` clause with `CREATE TABLE` or `CREATE TEMP TABLE`:

- If any transformation function generates a vector output, it is automatically converted to an array.
- As a result, tables created using `TRANSFORM` cannot be used directly in `CREATE MODEL` statements. You must redefine the transformation logic during model creation to generate the appropriate feature vectors.
- Transformations are only applied during table creation. I nuovi dati inseriti nella tabella con `INSERT INTO` sono **non trasformati automaticamente**. Per applicare le trasformazioni ai nuovi dati, è necessario ricreare la tabella utilizzando `CREATE TABLE AS SELECT` con la clausola `TRANSFORM`.
- Questo metodo ha lo scopo di visualizzare in anteprima e convalidare le trasformazioni in un determinato momento e non di creare pipeline di trasformazione riutilizzabili.

>[!NOTE]
>
>Per ulteriori dettagli sulle funzioni di trasformazione disponibili e sui relativi tipi di output, vedere [Tipi di dati di output di trasformazione delle funzionalità](../advanced-statistics/feature-transformation.md#available-transformations).


### clausola TRANSFORM {#transform}

Utilizzare la clausola `TRANSFORM` per applicare una o più funzioni di ingegneria delle funzionalità a un set di dati prima dell&#39;apprendimento del modello o della creazione di tabelle. Questa clausola consente di visualizzare in anteprima, convalidare o definire la forma esatta delle feature di input.

La clausola `TRANSFORM` può essere utilizzata nelle istruzioni seguenti:

- `CREATE MODEL`
- `CREATE TABLE`
- `CREATE TEMP TABLE`

Per istruzioni dettagliate sull&#39;utilizzo di CREATE MODEL, incluse le modalità di definizione delle trasformazioni, impostazione delle opzioni del modello e configurazione dei dati di formazione, vedere la [documentazione dei modelli](../advanced-statistics/models.md).

Per informazioni sull&#39;utilizzo di `CREATE TABLE`, vedere la sezione [CREATE TABLE AS SELECT](#create-table-as-select).

#### Esempio di creazione di un modello

```sql
CREATE MODEL review_model
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) AS ohe_add_comments,
  tokenizer(comments) AS token_comments,
  stop_words_remover(token_comments, array('and','very','much')) AS stp_token,
  ngram(stp_token, 3) AS ngram_token,
  tf_idf(ngram_token, 20) AS ngram_idf,
  count_vectorizer(stp_token, 13) AS cnt_vec_comments,
  tf_idf(token_comments, 10, 1) AS cmts_idf,
  vector_assembler(array(cmts_idf, viewsgot, ohe_add_comments, ngram_idf, cnt_vec_comments)) AS features
)
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='reviews')
AS SELECT * FROM movie_review_e2e_DND;
```

#### Limitazioni {#limitations}

Le seguenti limitazioni si applicano quando si utilizza `TRANSFORM` con `CREATE TABLE`. Consulta la sezione Limitazioni e comportamento di `CREATE TABLE AS SELECT` per una spiegazione dettagliata di come vengono memorizzati i dati trasformati, come vengono gestiti gli output vettoriali e perché i risultati non possono essere riutilizzati direttamente nei flussi di lavoro di formazione sui modelli.

- Gli output vettoriali vengono automaticamente convertiti in array, che non possono essere utilizzati direttamente in `CREATE MODEL`.
- La logica di trasformazione non viene resa persistente come metadati e non può essere riutilizzata in più batch.

## INSERISCI IN

Il comando `INSERT INTO` è definito come segue:

>[!IMPORTANT]
>
>Query Service supporta **operazioni di sola accodamento** tramite il motore ITAS. `INSERT INTO` è l&#39;unico comando di manipolazione dati supportato. Le operazioni **update** e **delete** non sono disponibili. Per riflettere le modifiche apportate ai dati, inserire nuovi record che rappresentino lo stato desiderato.

```sql
INSERT INTO table_name select_query
```

| Parametri | Descrizione |
| ----- | ----- |
| `table_name` | Nome della tabella in cui si desidera inserire la query. |
| `select_query` | Un&#39;istruzione `SELECT`. La sintassi della query `SELECT` si trova nella sezione [SELECT queries](#select-queries). |

**Esempio**

>[!NOTE]
>
>Quello che segue è un esempio inventato e semplicemente a scopo istruttivo.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>**not** racchiude l&#39;istruzione `SELECT` tra parentesi (). Inoltre, lo schema del risultato dell&#39;istruzione `SELECT` deve essere conforme a quello della tabella definita nell&#39;istruzione `INSERT INTO`. È possibile fornire una clausola `SNAPSHOT` per leggere i delta incrementali nella tabella di destinazione.

La maggior parte dei campi in uno schema XDM reale non viene trovata a livello principale e SQL non consente l’utilizzo della notazione del punto. Per ottenere un risultato realistico utilizzando campi nidificati, è necessario mappare ogni campo nel percorso `INSERT INTO`.

Per `INSERT INTO` percorsi nidificati, utilizzare la sintassi seguente:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Esempio**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## RILASCIA TABELLA

Il comando `DROP TABLE` elimina una tabella esistente ed elimina la directory associata alla tabella dal file system se non si tratta di una tabella esterna. Se la tabella non esiste, si verifica un&#39;eccezione.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se specificato, non viene generata alcuna eccezione se la tabella **non** esiste. |

## CREA DATABASE

Il comando `CREATE DATABASE` crea un database di Azure Data Lake Storage (ADLS).

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## ELIMINA DATABASE

Il comando `DROP DATABASE` elimina il database da un&#39;istanza.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se specificato, non viene generata alcuna eccezione se il database **non** esiste. |

## ELIMINA SCHEMA

Il comando `DROP SCHEMA` elimina uno schema esistente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se questo parametro è specificato e lo schema **non** esiste, non viene generata alcuna eccezione. |
| `RESTRICT` | Il valore predefinito per la modalità. Se specificato, lo schema viene eliminato solo se **non** contiene tabelle. |
| `CASCADE` | Se specificato, lo schema viene rilasciato insieme a tutte le tabelle presenti nello schema. |

## CREA VISUALIZZAZIONE {#create-view}

Una vista SQL è una tabella virtuale basata sul set di risultati di un&#39;istruzione SQL. Creare una visualizzazione con l&#39;istruzione `CREATE VIEW` e assegnarle un nome. È quindi possibile utilizzare tale nome per fare riferimento ai risultati della query. In questo modo è più semplice riutilizzare query complesse.

La sintassi seguente definisce una query `CREATE VIEW` per un set di dati. Questo set di dati può essere un ADLS o un set di dati archivio accelerato.

```sql
CREATE VIEW view_name AS select_query
```

| Parametri | Descrizione |
| ------ | ------ |
| `view_name` | Nome della visualizzazione da creare. |
| `select_query` | Un&#39;istruzione `SELECT`. La sintassi della query `SELECT` si trova nella sezione [SELECT queries](#select-queries). |

**Esempio**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

La sintassi seguente definisce una query `CREATE VIEW` che crea una visualizzazione nel contesto di un database e di uno schema.

**Esempio**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Parametri | Descrizione |
| ------ | ------ |
| `db_name` | Nome del database. |
| `schema_name` | Nome dello schema. |
| `view_name` | Nome della visualizzazione da creare. |
| `select_query` | Un&#39;istruzione `SELECT`. La sintassi della query `SELECT` si trova nella sezione [SELECT queries](#select-queries). |

**Esempio**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## MOSTRA VISTE

La query seguente mostra l’elenco delle visualizzazioni.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
|----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## VISTA A DISCESA

La sintassi seguente definisce una query `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se specificato, non viene generata alcuna eccezione se la visualizzazione **not** esiste. |
| `view_name` | Nome della visualizzazione da eliminare. |

**Esempio**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Blocco anonimo {#anonymous-block}

Un blocco anonimo è costituito da due sezioni: eseguibile e gestione delle eccezioni. In un blocco anonimo, la sezione eseguibile è obbligatoria. Tuttavia, la sezione relativa alla gestione delle eccezioni è facoltativa.

L’esempio seguente mostra come creare un blocco con una o più istruzioni da eseguire insieme:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHERS
      THEN statementList

statementList:
    : (statement (';')) +
```

Di seguito è riportato un esempio che utilizza un blocco anonimo.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHERS THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Istruzioni condizionali in un blocco anonimo {#conditional-anonymous-block-statements}

La struttura di controllo IF-THEN-ELSE consente l&#39;esecuzione condizionale di un elenco di istruzioni quando una condizione viene valutata come TRUE. Questa struttura di controllo è applicabile solo all&#39;interno di un blocco anonimo. Se questa struttura viene utilizzata come comando autonomo, si verifica un errore di sintassi (&quot;Comando non valido all&#39;esterno di Blocco anonimo&quot;).

Il frammento di codice seguente illustra il formato corretto per un&#39;istruzione condizionale IF-THEN-ELSE in un blocco anonimo.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Esempio**

L&#39;esempio seguente esegue `SELECT 200;`.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Questa struttura può essere utilizzata con `raise_error();` per restituire un messaggio di errore personalizzato. Il blocco di codice visualizzato di seguito termina il blocco anonimo con un &quot;messaggio di errore personalizzato&quot;.

**Esempio**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Istruzioni IF nidificate

Le istruzioni IF nidificate sono supportate all’interno di blocchi anonimi.

**Esempio**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Blocchi di eccezioni

I blocchi di eccezione sono supportati all’interno di blocchi anonimi.

**Esempio**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHERS THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Automatico a JSON {#auto-to-json}

Query Service supporta un’impostazione facoltativa a livello di sessione per restituire campi complessi di primo livello da query SELECT interattive come stringhe JSON. L&#39;impostazione `auto_to_json` consente di restituire dati da campi complessi come JSON e quindi analizzarli in oggetti JSON utilizzando librerie standard.

IMPOSTARE il flag di funzionalità `auto_to_json` su true prima di eseguire la query SELECT contenente campi complessi.

```sql
set auto_to_json=true; 
```

#### Prima di impostare il flag `auto_to_json`

Nella tabella seguente viene fornito un esempio di risultato della query prima dell&#39;applicazione dell&#39;impostazione `auto_to_json`. In entrambi gli scenari è stata utilizzata la stessa query SELECT (come mostrato di seguito) che esegue il targeting di una tabella con campi complessi.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

I risultati sono i seguenti:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
|-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Dopo aver impostato il flag `auto_to_json`

Nella tabella seguente viene illustrata la differenza di risultati dell&#39;impostazione `auto_to_json` nel set di dati risultante. In entrambi gli scenari è stata utilizzata la stessa query SELECT.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
|-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Risolvi snapshot di fallback in caso di errore {#resolve-fallback-snapshot-on-failure}

L&#39;opzione `resolve_fallback_snapshot_on_failure` viene utilizzata per risolvere il problema di un ID di snapshot scaduto.

Impostare l&#39;opzione `resolve_fallback_snapshot_on_failure` su true per sostituire uno snapshot con un ID snapshot precedente.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

La seguente riga di codice sostituisce `@from_snapshot_id` con il primo `snapshot_id` disponibile dai metadati.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHERS THEN
    SELECT 'ERROR';
END
$$;
```


## Organizzazione delle risorse dati

È importante organizzare in modo logico le risorse dati all’interno del data lake di Adobe Experience Platform man mano che crescono. Query Service estende i costrutti SQL che consentono di raggruppare in modo logico le risorse di dati all’interno di una sandbox. Questo metodo di organizzazione consente la condivisione di risorse di dati tra schemi senza la necessità di spostarli fisicamente.

I costrutti SQL seguenti che utilizzano la sintassi SQL standard sono supportati per organizzare in modo logico i dati.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consulta la [guida dell&#39;organizzazione logica delle risorse dati](../best-practices/organize-data-assets.md) per una spiegazione più dettagliata sulle best practice di Query Service.

## Tabella esistente

Il comando SQL `table_exists` viene utilizzato per confermare se una tabella esiste attualmente nel sistema. Il comando restituisce un valore booleano: `true` se la tabella **esiste** e `false` se la tabella **non** esiste.

Convalidando la presenza di una tabella prima di eseguire le istruzioni, la funzionalità `table_exists` semplifica il processo di scrittura di un blocco anonimo per coprire sia i casi d&#39;uso `CREATE` che quelli `INSERT INTO`.

La sintassi seguente definisce il comando `table_exists`:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN OTHERS THEN SELECT 'ERROR';

END $$; 
```

## In linea {#inline}

La funzione `inline` separa gli elementi di una matrice di strutture e genera i valori in una tabella. Può essere inserito solo nell&#39;elenco `SELECT` o in un `LATERAL VIEW`.

La funzione `inline` **non può** essere inserita in un elenco di selezione in cui sono presenti altre funzioni del generatore.

Per impostazione predefinita, le colonne prodotte sono denominate &quot;col1&quot;, &quot;col2&quot; e così via. Se l&#39;espressione è `NULL`, non verrà generata alcuna riga.

>[!TIP]
>
>I nomi di colonna possono essere rinominati utilizzando il comando `RENAME`.

**Esempio**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

Nell&#39;esempio viene restituito quanto segue:

```text
1  a Spark SQL
2  b Spark SQL
```

Questo secondo esempio illustra ulteriormente il concetto e l&#39;applicazione della funzione `inline`. Il modello dati per l’esempio è illustrato nell’immagine seguente.

![Diagramma di schema per productListItems.](../images/sql/productListItems.png)

**Esempio**

```sql
select inline(productListItems) from source_dataset limit 10;
```

I valori presi da `source_dataset` vengono utilizzati per popolare la tabella di destinazione.

| SKU | _experience | quantity | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## SET

The `SET` command sets a property and either returns the value of an existing property or lists all the existing properties. If a value is provided for an existing property key, the old value is overridden.

```sql
SET property_key = property_value
```

| Parametri | Descrizione |
| ------ | ------ |
| `property_key` | The name of the property that you want to list or alter. |
| `property_value` | The value that you want the property to be set as. |

To return the value for any setting, use `SET [property key]` without a `property_value`.

## [!DNL PostgreSQL] commands

The subsections below cover the [!DNL PostgreSQL] commands supported by Query Service.

### ANALYZE TABLE {#analyze-table}

The `ANALYZE TABLE` command performs a distribution analysis and statistical calculations for the named table or tables. The use of `ANALYZE TABLE` varies depending on whether the datasets are stored on the [accelerated store](#compute-statistics-accelerated-store) or the [data lake](#compute-statistics-data-lake). See their respective sections for more information on its use.

#### COMPUTE STATISTICS on the accelerated store {#compute-statistics-accelerated-store}

The `ANALYZE TABLE` command computes statistics for a table on the accelerated store. The statistics are calculated on executed CTAS or ITAS queries for a given table on the accelerated store.

**Esempio**

```sql
ANALYZE TABLE <original_table_name>
```

The following is a list of statistical calculations that are available after using the `ANALYZE TABLE` command:-

| Calculated values | Descrizione |
|---|---|
| `field` | The name of the column in a table. |
| `data-type` | The acceptable type of data for each column. |
| `count` | The number of rows that contain a non-null value for this field. |
| `distinct-count` | The number of unique or distinct values for this field. |
| `missing` | The number of rows that have a null value for this field. |
| `max` | The maximum value from the analyzed table. |
| `min` | The minimum value from the analyzed table. |
| `mean` | The average value of the analyzed table. |
| `stdev` | The standard deviation of the analyzed table. |

#### COMPUTE STATISTICS on the data lake {#compute-statistics-data-lake}

You can now calculate column-level statistics on [!DNL Azure Data Lake Storage] (ADLS) datasets with the `COMPUTE STATISTICS` SQL command. Compute column statistics on either the entire dataset, a subset of a dataset, all columns, or a subset of columns.

`COMPUTE STATISTICS` extends the `ANALYZE TABLE` command. However, the `COMPUTE STATISTICS`, `FILTERCONTEXT`, and `FOR COLUMNS` commands are not supported on accelerated store tables. These extensions for the `ANALYZE TABLE` command are currently only supported for ADLS tables.

**Esempio**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

The `FILTER CONTEXT` command calculates statistics on a subset of the dataset based on the filter condition provided. The `FOR COLUMNS` command targets specific columns for analysis.

>[!NOTE]
>
>The `Statistics ID` and the statistics generated are only valid for each session and cannot be accessed across different PSQL sessions.<br><br>Limitations:<ul><li>Statistics generation is not supported for array or map data types</li><li>Computed statistics are **not** persisted across sessions.</li></ul><br><br>Opzioni:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>By default, the flag is set to true. As a result, when statistics are requested on a datatype that is not supported, it does not error out but silently skips fields with the unsupported datatypes.<br>To enable notifications on errors when statistics are requested on unsupported datatype, use: `SET skip_stats_for_complex_datatypes = false`.

The console output appears as seen below.

```console
|     Statistics ID      |
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

You can then query the computed statistics directly by referencing the `Statistics ID`. Use the the `Statistics ID` or the alias name as shown in the example statement below, to view the output in full. To learn more about this feature, see the [alias name documentation](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Use the `SHOW STATISTICS` command to display the metadata for all the temporary statistics generated in the session. This command can help you refine the scope of your statistical analysis.

```sql
SHOW STATISTICS;
```

An example output of SHOW STATISTICS is seen below.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
|----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

See the [dataset statistics documentation](../key-concepts/dataset-statistics.md) for more information.

#### TABLESAMPLE {#tablesample}

Adobe Experience Platform Query Service provides sample datasets as part of its approximate query processing capabilities.

Data set samples are best used when you do not need an exact answer for an aggregate operation over a dataset. To conduct more efficient exploratory queries on large datasets by issuing an approximate query to return an approximate answer, use the `TABLESAMPLE` feature.

Sample datasets are created with uniform random samples from existing [!DNL Azure Data Lake Storage] (ADLS) datasets, using only a percentage of records from the original. The dataset sample feature extends the `ANALYZE TABLE` command with the `TABLESAMPLE` and `SAMPLERATE` SQL commands.

In the example below, line one demonstrates how to compute a 5% sample of the table. Line two demonstrates how to compute a 5% sample from a  filtered view of the data within the table.

**Esempio**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

See the [dataset samples documentation](../key-concepts/dataset-samples.md) for more information.

### BEGIN

The `BEGIN` command, or alternatively the `BEGIN WORK` or `BEGIN TRANSACTION` command, initiates a transaction block. Any statements that are inputted after the begin command will be executed in a single transaction until an explicit COMMIT or ROLLBACK command is given. This command is the same as `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

The `CLOSE` command frees the resources associated with an open cursor. After the cursor is closed, no subsequent operations are allowed on it. A cursor should be closed when it is no longer needed.

```sql
CLOSE name
CLOSE ALL
```

Se si utilizza `CLOSE name`, `name` rappresenta il nome di un cursore aperto che deve essere chiuso. Se si utilizza `CLOSE ALL`, tutti i cursori aperti verranno chiusi.

### DEALLOCARE

Per deallocare un&#39;istruzione SQL preparata in precedenza, utilizzare il comando `DEALLOCATE`. Se un&#39;istruzione preparata non è stata esplicitamente deallocata, verrà deallocata al termine della sessione. Ulteriori informazioni sulle istruzioni preparate sono disponibili nella sezione del comando [PREPARE](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Se si utilizza `DEALLOCATE name`, `name` rappresenta il nome dell&#39;istruzione preparata che deve essere deallocata. Se si utilizza `DEALLOCATE ALL`, tutte le istruzioni preparate vengono deallocate.

### DICHIARA

Il comando `DECLARE` consente a un utente di creare un cursore che può essere utilizzato per recuperare un numero limitato di righe da una query più grande. Dopo aver creato il cursore, le righe vengono recuperate da esso utilizzando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome del cursore da creare. |
| `query` | Comando `SELECT` o `VALUES` che fornisce le righe che devono essere restituite dal cursore. |

### ESEGUI

Il comando `EXECUTE` viene utilizzato per eseguire un&#39;istruzione preparata in precedenza. Poiché le istruzioni preparate esistono solo durante una sessione, l&#39;istruzione preparata deve essere stata creata da un&#39;istruzione `PREPARE` eseguita in precedenza nella sessione corrente. Ulteriori informazioni sull&#39;utilizzo delle istruzioni preparate sono disponibili nella sezione [`PREPARE` comando](#prepare).

Se l&#39;istruzione `PREPARE` che ha creato l&#39;istruzione ha specificato alcuni parametri, è necessario passare un set di parametri compatibile all&#39;istruzione `EXECUTE`. Se questi parametri non vengono passati, viene generato un errore.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome dell&#39;istruzione preparata da eseguire. |
| `parameter` | Valore effettivo di un parametro per l&#39;istruzione preparata. Deve essere un&#39;espressione che restituisce un valore compatibile con il tipo di dati di questo parametro, come determinato al momento della creazione dell&#39;istruzione preparata. Se sono presenti più parametri per l&#39;istruzione preparata, vengono separati da virgole. |

### SPIEGARE

Il comando `EXPLAIN` visualizza il piano di esecuzione per l&#39;istruzione fornita. Il piano di esecuzione mostra come verranno analizzate le tabelle a cui fa riferimento l’istruzione. Se si fa riferimento a più tabelle, vengono mostrati gli algoritmi di join utilizzati per riunire le righe richieste da ogni tabella di input.

```sql
EXPLAIN statement
```

Per definire il formato della risposta, utilizzare la parola chiave `FORMAT` con il comando `EXPLAIN`.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parametri | Descrizione |
| ------ | ------ |
| `FORMAT` | Utilizzare il comando `FORMAT` per specificare il formato di output. Le opzioni disponibili sono `TEXT` o `JSON`. L&#39;output non testuale contiene le stesse informazioni del formato di output del testo, ma è più semplice da analizzare per i programmi. Il valore predefinito di questo parametro è `TEXT`. |
| `statement` | Qualsiasi istruzione `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` o `CREATE MATERIALIZED VIEW AS` di cui si desidera visualizzare il piano di esecuzione. |

>[!IMPORTANT]
>
>Qualsiasi output restituito da un&#39;istruzione `SELECT` viene scartato quando viene eseguito con la parola chiave `EXPLAIN`. Altri effetti indesiderati dell’indicazione si verificano come al solito.

**Esempio**

L&#39;esempio seguente mostra il piano per una query semplice su una tabella con una singola colonna `integer` e 10000 righe:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
|---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### RECUPERA

Il comando `FETCH` recupera le righe utilizzando un cursore creato in precedenza.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `num_of_rows` | Numero di righe da recuperare. |
| `cursor_name` | Nome del cursore da cui si stanno recuperando le informazioni. |

### PREPARA {#prepare}

Il comando `PREPARE` consente di creare un&#39;istruzione preparata. Un&#39;istruzione preparata è un oggetto lato server che può essere utilizzato per creare modelli di istruzioni SQL simili.

Le istruzioni preparate possono accettare parametri, ovvero valori che vengono sostituiti nell&#39;istruzione quando viene eseguita. I parametri vengono indicati per posizione, utilizzando $1, $2 e così via, quando si utilizzano le istruzioni preparate.

Facoltativamente, puoi specificare un elenco di tipi di dati dei parametri. Se il tipo di dati di un parametro non è elencato, è possibile dedurlo dal contesto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome dell&#39;istruzione preparata. |
| `data_type` | I tipi di dati dei parametri dell&#39;istruzione preparata. Se il tipo di dati di un parametro non è elencato, è possibile dedurlo dal contesto. If you must add multiple data types, you can add them in a comma-separated list. |

### ROLLBACK

The `ROLLBACK` command undoes the current transaction and discards all the updates made by the transaction.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

The `SELECT INTO` command creates a new table and fills it with data computed by a query. The data is not returned to the client, as it is with a normal `SELECT` command. The new table&#39;s columns have the names and data types associated with the output columns of the `SELECT` command.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

More information about the standard SELECT query parameters can be found in the [SELECT query section](#select-queries). This section only lists parameters that are exclusive to the `SELECT INTO` command.

| Parametri | Descrizione |
| ------ | ------ |
| `TEMPORARY` o `TEMP` | An optional parameter. If the parameter is specified, the created table is a temporary table. |
| `UNLOGGED` | An optional parameter. If the parameter is specified, the created table is an unlogged table. More information about unlogged tables can be found in the [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | The name of the table to be created. |

**Esempio**

The following query creates a new table `films_recent` consisting of only recent entries from the table `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

The `SHOW` command displays the current setting of runtime parameters. These variables can be set using the `SET` statement, by editing the `postgresql.conf` configuration file, through the `PGOPTIONS` environmental variable (when using libpq or a libpq-based application), or through command-line flags when starting the Postgres server.

```sql
SHOW name
SHOW ALL
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | The name of the runtime parameter you want information about. Possible values for the runtime parameter include the following values:<br>`SERVER_VERSION`: This parameter shows the server&#39;s version number.<br>`SERVER_ENCODING`: This parameter shows the server-side character set encoding.<br>`LC_COLLATE`: This parameter shows the database&#39;s locale setting for collation (text ordering).<br>`LC_CTYPE`: This parameter shows the database&#39;s locale setting for character classification.<br>`IS_SUPERUSER`: This parameter shows if the current role has superuser privileges. |
| `ALL` | Show the values of all configuration parameters with descriptions. |

**Esempio**

The following query shows the current setting of the parameter `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
|-----------
 ISO, MDY
(1 row)
```

### COPY

Il comando `COPY` duplica l&#39;output di qualsiasi query `SELECT` in un percorso specificato. Affinché il comando venga eseguito correttamente, l&#39;utente deve avere accesso a questa posizione.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parametri | Descrizione |
| ------ | ------ |
| `query` | La query da copiare. |
| `format_name` | Formato in cui copiare la query. `format_name` può essere uno di `parquet`, `csv` o `json`. Il valore predefinito è `parquet`. |

>[!NOTE]
>
>Il percorso di output completo è `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### MODIFICA TABELLA {#alter-table}

Il comando `ALTER TABLE` consente di aggiungere o eliminare vincoli di chiave primaria o esterna e di aggiungere colonne alla tabella.

#### AGGIUNGI O RILASCIA VINCOLO

Le query SQL seguenti mostrano alcuni esempi di aggiunta o eliminazione di vincoli a una tabella. I vincoli di chiave primaria e chiave esterna possono essere aggiunti a più colonne con valori separati da virgola. Puoi creare chiavi composite trasmettendo due o più valori del nome della colonna, come illustrato negli esempi seguenti.

**Definire le chiavi primarie o composite**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**Definire una relazione tra tabelle basata su una o più chiavi**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**Definisci una colonna di identità**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Eliminare un vincolo, una relazione o un&#39;identità**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parametri | Descrizione |
| ------ | ------ |
| `table_name` | Nome della tabella che si sta modificando. |
| `column_name` | Nome della colonna a cui si sta aggiungendo un vincolo. |
| `referenced_table_name` | Nome della tabella a cui fa riferimento la chiave esterna. |
| `primary_column_name` | Nome della colonna a cui fa riferimento la chiave esterna. |

>[!NOTE]
>
>Lo schema della tabella deve essere univoco e non condiviso tra più tabelle. Inoltre, lo spazio dei nomi è obbligatorio per i vincoli di chiave primaria, identità primaria e identità.

#### Aggiungere o eliminare identità primarie e secondarie

Per aggiungere o eliminare vincoli per le colonne della tabella delle identità primaria e secondaria, utilizzare il comando `ALTER TABLE`.

The following examples add a primary identity and a secondary identity by adding constraints.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Identities can also be removed by dropping constraints, as seen in the example below.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

For more detailed information, see the document on [setting identities in an ad hoc datasets](../data-governance/ad-hoc-schema-identities.md).

#### ADD COLUMN

The following SQL queries show examples of adding columns to a table.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Supported data types

The following table lists the accepted data types for adding columns to a table with [!DNL Postgres SQL], XDM, and the [!DNL Accelerated Database Recovery] (ADR) in Azure SQL.

| --- | PSQL client | XDM | ADR | Descrizione |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | A numerical data type used to store large integers ranging from –9,223,372,036,854,775,807 to 9,223,372,036,854,775,807 in 8 bytes. |
| 2 | `integer` | `int4` | `integer` | A numerical data type used to store integers ranging from -2,147,483,648 to 2,147,483,647 in 4 bytes. |
| 3 | `smallint` | `int2` | `smallint` | A numerical data type used to store integers ranging from -32,768 to 215-1 32,767 in 2 bytes. |
| 4 | `tinyint` | `int1` | `tinyint` | A numerical data type used to store integers ranging from 0 to 255 in 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | A character data type that is of variable-size. `varchar` is best used when the sizes of the column data entries vary considerably. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` and `FLOAT` are valid synonyms for `DOUBLE PRECISION`. `double precision` is a floating-point data type. Floating-point values are stored in 8 bytes. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` is a valid synonym for `double precision`.`double precision` is a floating-point data type. Floating-point values are stored in 8 bytes. |
| 8 | `date` | `date` | `date` | The `date` data types are 4-byte stored calendar date values without any timestamp information. The range of valid dates is from 01-01-0001 to 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | A data type used to store an instant in time expressed as a calendar date and time of day. `datetime` includes the qualifiers of: year, month, day, hour, second, and fraction. A `datetime` declaration can include any subset of these time units that are joined in that sequence, or even comprise only a single time unit. |
| 10 | `char(len)` | `string` | `char(len)` | The `char(len)` keyword is used to indicate that the item is fixed-length character. |

#### ADD SCHEMA

The following SQL query shows an example of adding a table to a database / schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS tables and views cannot be added to DWH databases / schemas.


#### REMOVE SCHEMA

The following SQL query shows an example of removing a table from a database / schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> DWH tables and views cannot be removed from physically linked DWH databases / schemas.


**Parametri**

| Parametri | Descrizione |
| ------ | ------ |
| `table_name` | Nome della tabella che si sta modificando. |
| `column_name` | The name of the column you want to add. |
| `data_type` | The data type of the column you want to add. Supported data types include the following: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### SHOW PRIMARY KEYS

The `SHOW PRIMARY KEYS` command lists all the primary key constraints for the given database.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
|------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### SHOW FOREIGN KEYS

The `SHOW FOREIGN KEYS` command lists all the foreign key constraints for the given database.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
|------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### SHOW DATAGROUPS

The `SHOW DATAGROUPS` command returns a table of all associated databases. For each database, the table includes schema, group type, child type, child name, and child ID.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### SHOW DATAGROUPS FOR table

The `SHOW DATAGROUPS FOR 'table_name'` command returns a table of all associated databases that contain the parameter as its child. For each database, the table includes schema, group type, child type, child name, and child ID.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parametri**

- `table_name`: The name of the table that you want to find associated databases for.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
