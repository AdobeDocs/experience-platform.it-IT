---
keywords: Experience Platform;home;argomenti comuni;servizio query;servizio query;sintassi sql;sql;ctas;CTAS;Crea tabella come selezione
solution: Experience Platform
title: Sintassi SQL nel servizio query
topic-legacy: syntax
description: Questo documento mostra la sintassi SQL supportata da Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 33c45c53e2ff591e7b94be1b4b17c25d2fe9d497
workflow-type: tm+mt
source-wordcount: '3033'
ht-degree: 2%

---

# Sintassi SQL in Query Service

Adobe Experience Platform Query Service consente di utilizzare SQL ANSI standard per `SELECT` istruzioni e altri comandi limitati. Questo documento descrive la sintassi SQL supportata da [!DNL Query Service].

## Query SELECT {#select-queries}

La sintassi seguente definisce un `SELECT` query supportata da [!DNL Query Service]:

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

dove `from_item` può essere una delle seguenti opzioni:

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

e `grouping_element` può essere una delle seguenti opzioni:

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

e `with_query` è:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

Le sottosezioni seguenti forniscono dettagli sulle clausole aggiuntive che è possibile utilizzare nelle query, purché queste seguano il formato descritto sopra.

### Clausola SNAPSHOT

Questa clausola può essere utilizzata per leggere in modo incrementale i dati su una tabella basata sugli ID snapshot. Un ID snapshot è un indicatore di checkpoint rappresentato da un numero Long-type applicato a una tabella data lake ogni volta che i dati vengono scritti. La `SNAPSHOT` La clausola si collega alla relazione della tabella utilizzata accanto a.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Esempio

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Si prega di notare che `SNAPSHOT` Questa funzione utilizza un alias di tabella o di tabella, ma non viene eseguita su una sottoquery o una visualizzazione. A `SNAPSHOT` funziona ovunque `SELECT` è possibile applicare una query su una tabella.

Inoltre, puoi utilizzare `HEAD` e `TAIL` come valori di offset speciali per le clausole snapshot. Utilizzo `HEAD` fa riferimento a un offset prima della prima istantanea, mentre `TAIL` fa riferimento a un offset dopo l&#39;ultima istantanea.

>[!NOTE]
>
>Se esegui una query tra due ID snapshot e lo snapshot iniziale è scaduto, possono verificarsi i due scenari seguenti, a seconda del flag opzionale di comportamento di fallback (`resolve_fallback_snapshot_on_failure`) è impostata:
>
>- Se è impostato il flag opzionale per il comportamento di fallback, Query Service sceglierà la prima istantanea disponibile, la imposterà come istantanea iniziale e restituirà i dati tra la prima istantanea disponibile e lo snapshot finale specificato. Questi dati sono **inclusivo** della prima istantanea disponibile.
>
>- Se il flag di comportamento di fallback facoltativo non è impostato, viene restituito un errore.


### clausola WHERE

Per impostazione predefinita, le corrispondenze prodotte da un `WHERE` clausola di `SELECT` le query sono sensibili all’uso di maiuscole e minuscole. Se desideri che le corrispondenze non facciano distinzione tra maiuscole e minuscole, puoi utilizzare la parola chiave `ILIKE` anziché `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logica delle clausole LIKE e ILIKE è spiegata nella seguente tabella:

| Clausola | Operatore |
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

Questa query restituisce i clienti con nomi che iniziano in &quot;A&quot; o &quot;a&quot;.

### JOIN

A `SELECT` la query che utilizza i join ha la sintassi seguente:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIONE, INTERSECT ed ECCETTO

La `UNION`, `INTERSECT`e `EXCEPT` vengono utilizzate per combinare o escludere righe simili da due o più tabelle:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREA TABELLA COME SELEZIONA

La sintassi seguente definisce un `CREATE TABLE AS SELECT` (CTAS) query:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| Parametri | Descrizione |
| ----- | ----- |
| `schema` | Titolo dello schema XDM. Utilizzare questa clausola solo se si desidera utilizzare uno schema XDM esistente per il nuovo set di dati creato dalla query CTAS. |
| `rowvalidation` | (Facoltativo) Specifica se l’utente desidera la convalida a livello di riga di ogni nuovo batch acquisito per il nuovo set di dati creato. Il valore predefinito è `true`. |
| `select_query` | A `SELECT` istruzione. La sintassi del `SELECT` è possibile trovare nella [Sezione query SELECT](#select-queries). |

**Esempio**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>La `SELECT` l&#39;istruzione deve avere un alias per le funzioni di aggregazione, ad esempio `COUNT`, `SUM`, `MIN`e così via. Inoltre, la `SELECT` può essere fornita con o senza parentesi (). Puoi fornire un `SNAPSHOT` per leggere i delta incrementali nella tabella di destinazione.

## INSERISCI IN

La `INSERT INTO` Il comando è definito come segue:

```sql
INSERT INTO table_name select_query
```

| Parametri | Descrizione |
| ----- | ----- |
| `table_name` | Nome della tabella in cui si desidera inserire la query. |
| `select_query` | A `SELECT` istruzione. La sintassi del `SELECT` è possibile trovare nella [Sezione query SELECT](#select-queries). |

**Esempio**

>[!NOTE]
>
>Di seguito è riportato un esempio contraffatto e semplicemente a scopo istruttivo.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> La `SELECT` dichiarazione **non deve** tra parentesi (). Inoltre, lo schema del risultato del `SELECT` l&#39;istruzione deve essere conforme a quella della tabella definita nella `INSERT INTO` istruzione. Puoi fornire un `SNAPSHOT` per leggere i delta incrementali nella tabella di destinazione.

La maggior parte dei campi in uno schema XDM reale non viene trovata a livello principale e SQL non consente l&#39;utilizzo della notazione del punto. Per ottenere un risultato realistico utilizzando campi nidificati, devi mappare ogni campo nel `INSERT INTO` percorso.

A `INSERT INTO` percorsi nidificati, utilizza la sintassi seguente:

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

## TABELLA A DISCESA

La `DROP TABLE` elimina una tabella esistente e la directory associata alla tabella dal file system se non è una tabella esterna. Se la tabella non esiste, si verifica un&#39;eccezione.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se viene specificato, non viene generata alcuna eccezione se la tabella lo fa **not** esistono. |

## CREA DATABASE

La `CREATE DATABASE` crea un database ADLS.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DATABASE DI RILASCIO

La `DROP DATABASE` elimina il database da un&#39;istanza.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se viene specificato, non viene generata alcuna eccezione se il database esegue **not** esistono. |

## SCHEMA DI RILASCIO

La `DROP SCHEMA` consente di eliminare uno schema esistente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se viene specificato, non viene generata alcuna eccezione se lo schema non lo fa **not** esistono. |
| `RESTRICT` | Valore predefinito per la modalità. Se viene specificato, lo schema verrà eliminato solo se è **non** contenere eventuali tabelle. |
| `CASCADE` | Se viene specificato, lo schema verrà rilasciato insieme a tutte le tabelle presenti nello schema. |

## CREA VISTA

La sintassi seguente definisce un `CREATE VIEW` query:

```sql
CREATE VIEW view_name AS select_query
```

| Parametri | Descrizione |
| ------ | ------ |
| `view_name` | Nome della visualizzazione da creare. |
| `select_query` | A `SELECT` istruzione. La sintassi del `SELECT` è possibile trovare nella [Sezione query SELECT](#select-queries). |

**Esempio**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## VISTA A DISCESA

La sintassi seguente definisce un `DROP VIEW` query:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se viene specificato, non viene generata alcuna eccezione se la visualizzazione lo fa **not** esistono. |
| `view_name` | Nome della visualizzazione da eliminare. |

**Esempio**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Blocco anonimo

Un blocco anonimo è costituito da due sezioni: sezioni eseguibili e di gestione delle eccezioni. In un blocco anonimo, la sezione eseguibile è obbligatoria. Tuttavia, la sezione relativa alla gestione delle eccezioni è facoltativa.

L’esempio seguente mostra come creare un blocco con una o più istruzioni da eseguire insieme:

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Di seguito è riportato un esempio che utilizza un blocco anonimo.

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## Organizzazione delle risorse dati

È importante organizzare in modo logico le risorse di dati all’interno del data lake di Adobe Experience Platform man mano che crescono. Query Service estende i costrutti SQL che consentono di raggruppare in modo logico le risorse di dati all’interno di una sandbox. Questo metodo di organizzazione consente la condivisione di risorse di dati tra schemi senza la necessità di spostarle fisicamente.

I seguenti costrutti SQL che utilizzano la sintassi SQL standard sono supportati per organizzare i dati in modo logico.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Consulta la guida su [organizzazione logica delle risorse dati](../best-practices/organize-data-assets.md) per una spiegazione più dettagliata sulle best practice relative al servizio query.

## La tabella esiste

La `table_exists` Il comando SQL viene utilizzato per verificare se nel sistema esiste o meno una tabella. Il comando restituisce un valore booleano: `true` se la tabella **does** esistono e `false` se la tabella **not** esistono.

Convalidando l&#39;esistenza di una tabella prima di eseguire le istruzioni, il `table_exists` semplifica il processo di scrittura di un blocco anonimo per coprire entrambi i `CREATE` e `INSERT INTO` casi di utilizzo.

La sintassi seguente definisce il `table_exists` comando:

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
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## In linea {#inline}

La `inline` separa gli elementi di un array di strutture e genera i valori in una tabella. Può essere posizionato solo nel `SELECT` elenco o `LATERAL VIEW`.

La `inline` Funzione **impossibile** essere inserito in un elenco selezionato in cui sono presenti altre funzioni del generatore.

Per impostazione predefinita, le colonne prodotte sono denominate &quot;col1&quot;, &quot;col2&quot; e così via. Se l’espressione è `NULL` non si producono righe.

>[!TIP]
>
>I nomi delle colonne possono essere rinominati utilizzando `RENAME` comando.

**Esempio**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

L&#39;esempio restituisce quanto segue:

```text
1  a Spark SQL
2  b Spark SQL
```

Questo secondo esempio dimostra ulteriormente il concetto e l&#39;applicazione `inline` funzione . Il modello dati per l’esempio è illustrato nell’immagine seguente.

![Diagramma di schema per productListItems](../images/sql/productListItems.png)

**Esempio**

```sql
select inline(productListItems) from source_dataset limit 10;
```

I valori presi dal `source_dataset` vengono utilizzati per compilare la tabella di destinazione.

| SKU | _esperienza | quantità | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;)) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;)) |  |  |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D, NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA, NULL)&quot;)&quot;)&quot;)) | 3 | 12 |

## [!DNL Spark] Comandi SQL

La sottosezione seguente illustra i comandi SQL Spark supportati da Query Service.

### SET

La `SET` imposta una proprietà e restituisce il valore di una proprietà esistente oppure elenca tutte le proprietà esistenti. Se viene fornito un valore per una chiave di proprietà esistente, il valore precedente viene ignorato.

```sql
SET property_key = property_value
```

| Parametri | Descrizione |
| ------ | ------ |
| `property_key` | Nome della proprietà che si desidera elencare o modificare. |
| `property_value` | Il valore con cui si desidera impostare la proprietà. |

Per restituire il valore di qualsiasi impostazione, utilizza `SET [property key]` senza `property_value`.

## Comandi PostgreSQL

Le sottosezioni seguenti descrivono i comandi PostgreSQL supportati da Query Service.

### INIZIO

La `BEGIN` o, in alternativa, il `BEGIN WORK` o `BEGIN TRANSACTION` avvia un blocco di transazione. Tutte le istruzioni inserite dopo il comando start vengono eseguite in una singola transazione fino a quando non viene fornito un comando esplicito COMMIT o ROLLBACK. Questo comando è lo stesso di `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CHIUDI

La `CLOSE` libera le risorse associate a un cursore aperto. Dopo la chiusura del cursore, non sono consentite operazioni successive. Quando non è più necessario, il cursore deve essere chiuso.

```sql
CLOSE name
CLOSE ALL
```

Se `CLOSE name` è utilizzato, `name` rappresenta il nome di un cursore aperto che deve essere chiuso. Se `CLOSE ALL` viene utilizzato, tutti i cursori aperti verranno chiusi.

### DEALLOCARE

La `DEALLOCATE` consente di deallocare un&#39;istruzione SQL preparata in precedenza. Se l&#39;istruzione preparata non viene deallocata in modo esplicito, al termine della sessione viene deallocata. Ulteriori informazioni sulle istruzioni preparate sono disponibili nella sezione [PREPARA, comando](#prepare) sezione .

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Se `DEALLOCATE name` è utilizzato, `name` rappresenta il nome dell&#39;istruzione preparata che deve essere deallocata. Se `DEALLOCATE ALL` viene utilizzato, tutte le istruzioni preparate verranno deallocate.

### DICHIARARE

La `DECLARE` consente a un utente di creare un cursore, che può essere utilizzato per recuperare un numero ridotto di righe da una query più grande. Una volta creato il cursore, le righe vengono recuperate da esso utilizzando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome del cursore da creare. |
| `query` | A `SELECT` o `VALUES` che fornisce le righe che devono essere restituite dal cursore. |

### ESEGUIRE

La `EXECUTE` viene utilizzato per eseguire un&#39;istruzione preparata in precedenza. Poiché le istruzioni preparate esistono solo per la durata di una sessione, l’istruzione preparata deve essere stata creata da un `PREPARE` istruzione eseguita in precedenza nella sessione corrente. Ulteriori informazioni sull’utilizzo delle istruzioni preparate sono disponibili nella sezione [`PREPARE` command](#prepare) sezione .

Se la `PREPARE` istruzione che ha creato l&#39;istruzione ha specificato alcuni parametri e un set di parametri compatibile deve essere trasmesso a `EXECUTE` istruzione. Se questi parametri non vengono passati, viene generato un errore.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome dell&#39;istruzione preparata da eseguire. |
| `parameter` | Il valore effettivo di un parametro per l&#39;istruzione preparata. Deve essere un&#39;espressione che produce un valore compatibile con il tipo di dati di questo parametro, come determinato al momento della creazione dell&#39;istruzione preparata.  Se l&#39;istruzione preparata contiene più parametri, questi saranno separati da virgole. |

### SPIEGARE

La `EXPLAIN` visualizza il piano di esecuzione per l&#39;istruzione fornita. Il piano di esecuzione mostra come verranno analizzate le tabelle a cui fa riferimento l&#39;istruzione.  Se si fa riferimento a più tabelle, verrà visualizzato quale algoritmo di join viene utilizzato per unire le righe richieste da ogni tabella di input.

```sql
EXPLAIN statement
```

Utilizza la `FORMAT` con la parola chiave `EXPLAIN` per definire il formato della risposta.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parametri | Descrizione |
| ------ | ------ |
| `FORMAT` | Utilizza la `FORMAT` per specificare il formato di output. Le opzioni disponibili sono `TEXT` o `JSON`. L&#39;output non testuale contiene le stesse informazioni del formato di output del testo, ma è più semplice da analizzare per i programmi. Il parametro predefinito è `TEXT`. |
| `statement` | Qualsiasi `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`oppure `CREATE MATERIALIZED VIEW AS` istruzione, di cui si desidera visualizzare il piano di esecuzione. |

>[!IMPORTANT]
>
>Qualsiasi output che `SELECT` l&#39;istruzione potrebbe restituire viene scartata quando viene eseguita con `EXPLAIN` keyword. Altri effetti collaterali dell&#39;istruzione avvengono come al solito.

**Esempio**

L’esempio seguente mostra il piano per una semplice query su una tabella con un singolo `integer` e 10000 righe:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### RECUPERO

La `FETCH` recupera le righe utilizzando un cursore creato in precedenza.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parametri | Descrizione |
| ------ | ------ |
| `num_of_rows` | Numero di righe da recuperare. |
| `cursor_name` | Nome del cursore da cui si recuperano le informazioni. |

### PREPARARE {#prepare}

La `PREPARE` consente di creare un&#39;istruzione preparata. Un&#39;istruzione preparata è un oggetto lato server che può essere utilizzato per modellare istruzioni SQL simili.

Le istruzioni preparate possono accettare parametri, ovvero valori che vengono sostituiti nell’istruzione al momento dell’esecuzione. I parametri vengono indicati in base alla posizione, utilizzando $ 1, $ 2 e così via, quando si utilizzano istruzioni preparate.

Facoltativamente, puoi specificare un elenco di tipi di dati dei parametri. Se il tipo di dati di un parametro non è elencato, il tipo può essere dedotto dal contesto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Nome dell&#39;istruzione preparata. |
| `data_type` | I tipi di dati dei parametri dell&#39;istruzione preparata. Se il tipo di dati di un parametro non è elencato, il tipo può essere dedotto dal contesto. Se devi aggiungere più tipi di dati, puoi aggiungerli in un elenco separato da virgole. |

### ROLLBACK

La `ROLLBACK` annulla la transazione corrente ed elimina tutti gli aggiornamenti effettuati dalla transazione.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELEZIONA IN

La `SELECT INTO` crea una nuova tabella e la riempie con i dati calcolati da una query. I dati non vengono restituiti al client, in quanto sono con una normale `SELECT` comando. Le colonne della nuova tabella presentano i nomi e i tipi di dati associati alle colonne di output della tabella `SELECT` comando.

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

Ulteriori informazioni sui parametri di query SELECT standard sono disponibili nella sezione [Sezione query SELECT](#select-queries). Questa sezione elencherà solo i parametri esclusivi per `SELECT INTO` comando.

| Parametri | Descrizione |
| ------ | ------ |
| `TEMPORARY` oppure `TEMP` | Un parametro facoltativo. Se specificato, la tabella creata sarà una tabella temporanea. |
| `UNLOGGED` | Un parametro facoltativo. Se specificato, la tabella creata come sarà una tabella non registrata. Ulteriori informazioni sulle tabelle non registrate sono disponibili in [Documentazione PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Nome della tabella da creare. |

**Esempio**

La seguente query crea una nuova tabella `films_recent` costituito solo da voci recenti della tabella `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRA

La `SHOW` visualizza l&#39;impostazione corrente dei parametri di runtime. Queste variabili possono essere impostate utilizzando `SET` , modificando `postgresql.conf` file di configurazione, attraverso `PGOPTIONS` variabile ambientale (quando si utilizza libpq o un&#39;applicazione basata su libpq) o tramite flag della riga di comando all&#39;avvio del server Postgres.

```sql
SHOW name
SHOW ALL
```

| Parametri | Descrizione |
| ------ | ------ |
| `name` | Il nome del parametro di runtime di cui si desidera ottenere informazioni. I valori possibili per il parametro runtime includono i seguenti valori:<br>`SERVER_VERSION`: Questo parametro mostra il numero di versione del server.<br>`SERVER_ENCODING`: Questo parametro mostra la codifica del set di caratteri lato server.<br>`LC_COLLATE`: Questo parametro mostra le impostazioni internazionali del database per le regole di confronto (ordinamento del testo).<br>`LC_CTYPE`: Questo parametro mostra le impostazioni internazionali del database per la classificazione dei caratteri.<br>`IS_SUPERUSER`: Questo parametro mostra se il ruolo corrente dispone di privilegi di utente avanzato. |
| `ALL` | Mostra i valori di tutti i parametri di configurazione con le descrizioni. |

**Esempio**

La seguente query mostra l’impostazione corrente del parametro `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### COPIA

La `COPY` duplica l&#39;output di qualsiasi `SELECT` eseguire una query in una posizione specificata. Per il corretto funzionamento di questo comando, l&#39;utente deve avere accesso a questa posizione.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parametri | Descrizione |
| ------ | ------ |
| `query` | Query da copiare. |
| `format_name` | Formato in cui si desidera copiare la query. La `format_name` può essere uno di `parquet`, `csv`oppure `json`. Per impostazione predefinita, il valore è `parquet`. |

>[!NOTE]
>
>Il percorso di output completo sarà `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### TABELLA ALTERNATIVA {#alter-table}

La `ALTER TABLE` consente di aggiungere o eliminare vincoli di chiave primaria o esterna e di aggiungere colonne alla tabella.


#### AGGIUNGI O RILASCIA VINCOLO

Le seguenti query SQL mostrano esempi di aggiunta o rilascio di vincoli a una tabella.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

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
>Lo schema della tabella deve essere univoco e non deve essere condiviso tra più tabelle. Inoltre, lo spazio dei nomi è obbligatorio per i vincoli di chiave primaria, identità primaria e identità.

#### Aggiungi o rilascia identità principali e secondarie

La `ALTER TABLE` consente di aggiungere o eliminare vincoli per le colonne della tabella di identità primaria e secondaria direttamente tramite SQL.

Negli esempi seguenti vengono aggiunte un&#39;identità principale e un&#39;identità secondaria tramite l&#39;aggiunta di vincoli.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

È inoltre possibile rimuovere le identità eliminando i vincoli, come illustrato nell’esempio seguente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Visualizza il documento in [impostazione delle identità in un set di dati ad hoc](../data-governance/ad-hoc-schema-identities.md) per informazioni più dettagliate.

#### AGGIUNGI COLONNA

Le seguenti query SQL mostrano esempi di aggiunta di colonne a una tabella.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Tipi di dati supportati

Nella tabella seguente sono elencati i tipi di dati accettati per l’aggiunta di colonne a una tabella con [!DNL Postgres SQL], XDM e [!DNL Accelerated Database Recovery] (ADR) in SQL di Azure.

| — | Client PSQL | XDM | ADR | Descrizione |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Tipo di dati numerico utilizzato per memorizzare interi di grandi dimensioni compresi tra -9.223.372.036.854.775.807 e 9.223.372.036.854.775.807 in 8 byte. |
| 2 | `integer` | `int4` | `integer` | Tipo di dati numerico utilizzato per memorizzare numeri interi compresi tra -2.147.483.648 e 2.147.483.647 in 4 byte. |
| 3 | `smallint` | `int2` | `smallint` | Tipo di dati numerico utilizzato per memorizzare numeri interi compresi tra -32.768 e 215-1 32.767 in 2 byte. |
| 4 | `tinyint` | `int1` | `tinyint` | Tipo di dati numerico utilizzato per memorizzare numeri interi compresi tra 0 e 255 in 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Tipo di dati carattere di dimensioni variabili. `varchar` viene utilizzato al meglio quando le dimensioni delle voci dei dati della colonna variano notevolmente. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` e `FLOAT` sono sinonimi validi per `DOUBLE PRECISION`. `double precision` è un tipo di dati a virgola mobile. I valori a virgola mobile vengono memorizzati in 8 byte. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` è un sinonimo valido per `double precision`.`double precision` è un tipo di dati a virgola mobile. I valori a virgola mobile vengono memorizzati in 8 byte. |
| 8 | `date` | `date` | `date` | La `date` il tipo di dati è costituito da valori di data del calendario memorizzati a 4 byte senza informazioni sulle marche temporali. L&#39;intervallo di date valide è compreso tra 01-01-0001 e 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Tipo di dati utilizzato per memorizzare un istante nel tempo espresso come data e ora del giorno del calendario. `datetime` include i qualificatori di: anno, mese, giorno, ora, secondo e frazione. A `datetime` La dichiarazione può includere qualsiasi sottoinsieme di queste unità temporali che sono unite in quella sequenza, o anche includere una sola unità di tempo. |
| 10 | `char(len)` | `string` | `char(len)` | La `char(len)` viene utilizzato per indicare che l&#39;elemento è un carattere a lunghezza fissa. |

#### AGGIUNGI SCHEMA

La seguente query SQL mostra un esempio di aggiunta di una tabella a un database o a uno schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Impossibile aggiungere tabelle e viste ADLS ai database/schemi DWH.


#### RIMUOVI SCHEMA

La seguente query SQL mostra un esempio di rimozione di una tabella da un database/schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Le tabelle e le viste DWH non possono essere rimosse dai database/schemi DWH collegati fisicamente.


**Parametri**

| Parametri | Descrizione |
| ------ | ------ |
| `table_name` | Nome della tabella che si sta modificando. |
| `column_name` | Nome della colonna da aggiungere. |
| `data_type` | Il tipo di dati della colonna da aggiungere. I tipi di dati supportati includono: bigint, char, stringa, data, datetime, doppio, precisione doppia, numero intero, piccolo, tinyint, varchar. |

### MOSTRA CHIAVI PRINCIPALI

La `SHOW PRIMARY KEYS` elenca tutti i vincoli di chiave primaria per il database specificato.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### MOSTRA CHIAVI ESTERNE

La `SHOW FOREIGN KEYS` elenca tutti i vincoli di chiave esterna per il database specificato.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### MOSTRA GRUPPI DI DATI

La `SHOW DATAGROUPS` restituisce una tabella di tutti i database associati. Per ogni database la tabella include schema, tipo di gruppo, tipo figlio, nome figlio e ID figlio.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### MOSTRA GRUPPI DI DATI PER LA TABELLA

La `SHOW DATAGROUPS FOR` Il comando &#39;table_name&#39; restituisce una tabella di tutti i database associati che contengono il parametro come figlio. Per ogni database la tabella include schema, tipo di gruppo, tipo figlio, nome figlio e ID figlio.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parametri**

- `table_name`: Nome della tabella per la quale si desidera trovare i database associati.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
