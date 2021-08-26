---
keywords: Experience Platform;home;argomenti comuni;servizio query;servizio query;sintassi sql;sql;ctas;CTAS;Crea tabella come selezione
solution: Experience Platform
title: Sintassi SQL nel servizio query
topic-legacy: syntax
description: Questo documento mostra la sintassi SQL supportata da Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 8dceab8cdba1ac6b4a649f0e01b2bbda5f025bef
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 1%

---

# Sintassi SQL in Query Service

Adobe Experience Platform Query Service consente di utilizzare SQL ANSI standard per le istruzioni `SELECT` e altri comandi limitati. Questo documento descrive la sintassi SQL supportata da [!DNL Query Service].

## Query SELECT {#select-queries}

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

e `grouping_element` possono essere una delle seguenti opzioni:

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

Questa clausola può essere utilizzata per leggere in modo incrementale i dati su una tabella basata sugli ID snapshot. Un ID snapshot è un indicatore di checkpoint rappresentato da un numero Long-type applicato a una tabella data lake ogni volta che i dati vengono scritti. La clausola `SNAPSHOT` si attacca alla relazione della tabella che viene utilizzata accanto a.

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

Nota che una clausola `SNAPSHOT` funziona con un alias di tabella o tabella ma non sopra una sottoquery o una visualizzazione. Una clausola `SNAPSHOT` funziona ovunque sia possibile applicare una query `SELECT` su una tabella.

Inoltre, è possibile utilizzare `HEAD` e `TAIL` come valori di offset speciali per le clausole snapshot. Utilizzando `HEAD` si fa riferimento a un offset prima della prima istantanea, mentre `TAIL` fa riferimento a un offset dopo l&#39;ultima istantanea.

>[!NOTE]
>
>Se si esegue una query tra due ID snapshot e lo snapshot iniziale è scaduto, possono verificarsi i due scenari seguenti, a seconda che sia impostato il flag opzionale di comportamento di fallback (`resolve_fallback_snapshot_on_failure`):
>
>- Se è impostato il flag opzionale per il comportamento di fallback, Query Service sceglierà la prima istantanea disponibile, la imposterà come istantanea iniziale e restituirà i dati tra la prima istantanea disponibile e lo snapshot finale specificato. Questi dati sono **inclusi** della prima istantanea disponibile.
>
>- Se il flag di comportamento di fallback facoltativo non è impostato, viene restituito un errore.


### clausola WHERE

Per impostazione predefinita, le corrispondenze prodotte da una clausola `WHERE` in una query `SELECT` sono sensibili all’uso di maiuscole e minuscole. Se desideri che le corrispondenze non facciano distinzione tra maiuscole e minuscole, puoi utilizzare la parola chiave `ILIKE` invece di `LIKE`.

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

Una query `SELECT` che utilizza join ha la seguente sintassi:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNIONE, INTERSECT ed ECCETTO

Le clausole `UNION`, `INTERSECT` e `EXCEPT` vengono utilizzate per combinare o escludere righe simili da due o più tabelle:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREA TABELLA COME SELEZIONA

La sintassi seguente definisce una query `CREATE TABLE AS SELECT` (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parametri**

- `schema`: Titolo dello schema XDM. Utilizzare questa clausola solo se si desidera utilizzare uno schema XDM esistente per il nuovo set di dati creato dalla query CTAS.
- `rowvalidation`: (Facoltativo) Specifica se l’utente desidera la convalida a livello di riga di ogni nuovo batch acquisito per il nuovo set di dati creato. Il valore predefinito è `true`.
- `select_query`: Un&#39; `SELECT` istruzione. La sintassi della query `SELECT` si trova nella sezione [SELECT query](#select-queries).

**Esempio**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>L&#39;istruzione `SELECT` deve avere un alias per le funzioni di aggregazione come `COUNT`, `SUM`, `MIN` e così via. Inoltre, l’istruzione `SELECT` può essere fornita con o senza parentesi (). È possibile fornire una clausola `SNAPSHOT` per leggere le delta incrementali nella tabella di destinazione.

## INSERISCI IN

Il comando `INSERT INTO` è definito come segue:

```sql
INSERT INTO table_name select_query
```

**Parametri**

- `table_name`: Nome della tabella in cui si desidera inserire la query.
- `select_query`: Un&#39; `SELECT` istruzione. La sintassi della query `SELECT` si trova nella sezione [SELECT query](#select-queries).

**Esempio**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> L&#39;istruzione `SELECT` **non deve** essere racchiusa tra parentesi (). Inoltre, lo schema del risultato dell&#39;istruzione `SELECT` deve essere conforme a quello della tabella definita nell&#39;istruzione `INSERT INTO`. È possibile fornire una clausola `SNAPSHOT` per leggere le delta incrementali nella tabella di destinazione.

## TABELLA A DISCESA

Il comando `DROP TABLE` rilascia una tabella esistente ed elimina dal file system la directory associata alla tabella se non è una tabella esterna. Se la tabella non esiste, si verifica un&#39;eccezione.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parametri**

- `IF EXISTS`: Se viene specificato, non viene generata alcuna eccezione se la tabella  **** non esiste.

## DATABASE DI RILASCIO

Il comando `DROP DATABASE` rilascia un database esistente.

```sql
DROP DATABASE [IF EXISTS] db_name
```

**Parametri**

- `IF EXISTS`: Se viene specificato, non viene generata alcuna eccezione se il database  **** non esiste.

## SCHEMA DI RILASCIO

Il comando `DROP SCHEMA` rilascia uno schema esistente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**Parametri**

- `IF EXISTS`: Se viene specificato, non viene generata alcuna eccezione se lo schema  **** non esiste.

- `RESTRICT`: Valore predefinito per la modalità. Se viene specificato, lo schema verrà eliminato solo se **non** contiene tabelle.

- `CASCADE`: Se viene specificato, lo schema verrà rilasciato insieme a tutte le tabelle presenti nello schema.

## CREA VISTA

La sintassi seguente definisce una query `CREATE VIEW` :

```sql
CREATE VIEW view_name AS select_query
```

**Parametri**

- `view_name`: Nome della visualizzazione da creare.
- `select_query`: Un&#39; `SELECT` istruzione. La sintassi della query `SELECT` si trova nella sezione [SELECT query](#select-queries).

**Esempio**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## VISTA A DISCESA

La sintassi seguente definisce una query `DROP VIEW` :

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parametro**

- `IF EXISTS`: Se viene specificato, non viene generata alcuna eccezione se la visualizzazione  **** non esiste.
- `view_name`: Nome della visualizzazione da eliminare.

**Esempio**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Comandi SQL

La sottosezione seguente illustra i comandi SQL Spark supportati da Query Service.

### SET

Il comando `SET` imposta una proprietà e restituisce il valore di una proprietà esistente oppure elenca tutte le proprietà esistenti. Se viene fornito un valore per una chiave di proprietà esistente, il valore precedente viene ignorato.

```sql
SET property_key = property_value
```

**Parametri**

- `property_key`: Nome della proprietà che si desidera elencare o modificare.
- `property_value`: Il valore con cui si desidera impostare la proprietà.

Per restituire il valore di qualsiasi impostazione, utilizza `SET [property key]` senza `property_value`.

## Comandi PostgreSQL

Le sottosezioni seguenti descrivono i comandi PostgreSQL supportati da Query Service.

### INIZIO

Il comando `BEGIN`, o in alternativa il comando `BEGIN WORK` o `BEGIN TRANSACTION`, avvia un blocco di transazione. Tutte le istruzioni inserite dopo il comando start vengono eseguite in una singola transazione fino a quando non viene fornito un comando esplicito COMMIT o ROLLBACK. Questo comando è lo stesso di `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CHIUDI

Il comando `CLOSE` consente di liberare le risorse associate a un cursore aperto. Dopo la chiusura del cursore, non sono consentite operazioni successive. Quando non è più necessario, il cursore deve essere chiuso.

```sql
CLOSE name
CLOSE ALL
```

Se si utilizza `CLOSE name`, `name` rappresenta il nome di un cursore aperto che deve essere chiuso. Se si utilizza `CLOSE ALL`, tutti i cursori aperti verranno chiusi.

### DEALLOCARE

Il comando `DEALLOCATE` consente di deallocare un&#39;istruzione SQL preparata in precedenza. Se l&#39;istruzione preparata non viene deallocata in modo esplicito, al termine della sessione viene deallocata. Ulteriori informazioni sulle istruzioni preparate sono disponibili nella sezione [Comando PREPARE](#prepare) .

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Se si utilizza `DEALLOCATE name`, `name` rappresenta il nome dell&#39;istruzione preparata che deve essere deallocata. Se si utilizza `DEALLOCATE ALL`, tutte le istruzioni preparate verranno deallocate.

### DICHIARARE

Il comando `DECLARE` consente all&#39;utente di creare un cursore, che può essere utilizzato per recuperare un numero limitato di righe da una query più grande. Una volta creato il cursore, le righe vengono recuperate da esso utilizzando `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

**Parametri**

- `name`: Nome del cursore da creare.
- `query`: Un  `SELECT` comando  `VALUES` o che fornisce le righe che devono essere restituite dal cursore.

### ESEGUIRE

Il comando `EXECUTE` viene utilizzato per eseguire un&#39;istruzione preparata in precedenza. Poiché le istruzioni preparate esistono solo per la durata di una sessione, l’istruzione preparata deve essere stata creata da un’istruzione `PREPARE` eseguita in precedenza nella sessione corrente. Ulteriori informazioni sull&#39;utilizzo delle istruzioni preparate sono disponibili nella sezione [`PREPARE` command](#prepare) .

Se l’istruzione `PREPARE` che ha creato l’istruzione ha specificato alcuni parametri, è necessario trasmettere un set di parametri compatibile all’istruzione `EXECUTE`. Se questi parametri non vengono passati, viene generato un errore.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parametri**

- `name`: Nome dell&#39;istruzione preparata da eseguire.
- `parameter`: Il valore effettivo di un parametro per l&#39;istruzione preparata. Deve essere un&#39;espressione che produce un valore compatibile con il tipo di dati di questo parametro, come determinato al momento della creazione dell&#39;istruzione preparata.  Se l&#39;istruzione preparata contiene più parametri, questi saranno separati da virgole.

### SPIEGARE

Il comando `EXPLAIN` visualizza il piano di esecuzione per l&#39;istruzione fornita. Il piano di esecuzione mostra come verranno analizzate le tabelle a cui fa riferimento l&#39;istruzione.  Se si fa riferimento a più tabelle, verrà visualizzato quale algoritmo di join viene utilizzato per unire le righe richieste da ogni tabella di input.

```sql
EXPLAIN option statement
```

Dove `option` può essere uno dei seguenti:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parametri**

- `ANALYZE`: Se la  `option` contiene  `ANALYZE`, vengono visualizzati i tempi di esecuzione e altre statistiche.
- `FORMAT`: Se il  `option` contiene  `FORMAT`, specifica il formato di output, che può essere  `TEXT` o  `JSON`. L&#39;output non testuale contiene le stesse informazioni del formato di output del testo, ma è più semplice da analizzare per i programmi. Il valore predefinito di questo parametro è `TEXT`.
- `statement`: Qualsiasi  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS` o  `CREATE MATERIALIZED VIEW AS` istruzione di cui si desidera visualizzare il piano di esecuzione.

>[!IMPORTANT]
>
>Tenere presente che l’istruzione viene effettivamente eseguita quando si utilizza l’opzione `ANALYZE` . Sebbene `EXPLAIN` scarti qualsiasi output restituito da un `SELECT`, altri effetti collaterali dell&#39;istruzione si verificano normalmente.

**Esempio**

L’esempio seguente mostra il piano di una semplice query su una tabella con una singola colonna `integer` e 10000 righe:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### RECUPERO

Il comando `FETCH` recupera le righe utilizzando un cursore creato in precedenza.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parametri**

- `num_of_rows`: Numero di righe da recuperare.
- `cursor_name`: Nome del cursore da cui si recuperano le informazioni.

### PREPARARE {#prepare}

Il comando `PREPARE` consente di creare un&#39;istruzione preparata. Un&#39;istruzione preparata è un oggetto lato server che può essere utilizzato per modellare istruzioni SQL simili.

Le istruzioni preparate possono accettare parametri, ovvero valori che vengono sostituiti nell’istruzione al momento dell’esecuzione. I parametri vengono indicati in base alla posizione, utilizzando $ 1, $ 2 e così via, quando si utilizzano istruzioni preparate.

Facoltativamente, puoi specificare un elenco di tipi di dati dei parametri. Se il tipo di dati di un parametro non è elencato, il tipo può essere dedotto dal contesto.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parametri**

- `name`: Nome dell&#39;istruzione preparata.
- `data_type`: I tipi di dati dei parametri dell&#39;istruzione preparata. Se il tipo di dati di un parametro non è elencato, il tipo può essere dedotto dal contesto. Se devi aggiungere più tipi di dati, puoi aggiungerli in un elenco separato da virgole.

### ROLLBACK

Il comando `ROLLBACK` annulla la transazione corrente ed elimina tutti gli aggiornamenti effettuati dalla transazione.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELEZIONA IN

Il comando `SELECT INTO` crea una nuova tabella e la riempie con i dati calcolati da una query. I dati non vengono restituiti al client, come avviene con un normale comando `SELECT`. Le colonne della nuova tabella presentano i nomi e i tipi di dati associati alle colonne di output del comando `SELECT`.

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

**Parametri**

Ulteriori informazioni sui parametri di query SELECT standard sono disponibili nella sezione [SELECT query](#select-queries). Questa sezione elenca solo i parametri esclusivi del comando `SELECT INTO`.

- `TEMPORARY` o  `TEMP`: Un parametro facoltativo. Se specificato, la tabella creata sarà una tabella temporanea.
- `UNLOGGED`: Un parametro facoltativo. Se specificato, la tabella creata come sarà una tabella non registrata. Ulteriori informazioni sulle tabelle non registrate sono disponibili nella [documentazione PostgreSQL](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Nome della tabella da creare.

**Esempio**

La seguente query crea una nuova tabella `films_recent` costituita solo da voci recenti della tabella `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRA

Il comando `SHOW` visualizza l&#39;impostazione corrente dei parametri di runtime. Queste variabili possono essere impostate utilizzando l&#39;istruzione `SET`, modificando il file di configurazione `postgresql.conf`, attraverso la variabile ambientale `PGOPTIONS` (quando si utilizza libpq o un&#39;applicazione basata su libpq) o tramite i flag della riga di comando all&#39;avvio del server Postgres.

```sql
SHOW name
SHOW ALL
```

**Parametri**

- `name`: Nome del parametro di runtime di cui si desidera ottenere informazioni. I valori possibili per il parametro runtime includono i seguenti valori:
   - `SERVER_VERSION`: Questo parametro mostra il numero di versione del server.
   - `SERVER_ENCODING`: Questo parametro mostra la codifica del set di caratteri lato server.
   - `LC_COLLATE`: Questo parametro mostra le impostazioni internazionali del database per le regole di confronto (ordinamento del testo).
   - `LC_CTYPE`: Questo parametro mostra le impostazioni internazionali del database per la classificazione dei caratteri.
      `IS_SUPERUSER`: Questo parametro mostra se il ruolo corrente dispone di privilegi di utente avanzato.
- `ALL`: Mostra i valori di tutti i parametri di configurazione con le descrizioni.

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

Il comando `COPY` scarica l&#39;output di qualsiasi query `SELECT` in una posizione specificata. Per il corretto funzionamento di questo comando, l&#39;utente deve avere accesso a questa posizione.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parametri**

- `query`: Query da copiare.
- `format_name`: Formato in cui si desidera copiare la query. Il `format_name` può essere compreso tra `parquet`, `csv` o `json`. Per impostazione predefinita, il valore è `parquet`.

>[!NOTE]
>
>Il percorso di output completo sarà `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### TABELLA ALTERNATIVA

Il comando `ALTER TABLE` consente di aggiungere o eliminare vincoli di chiave primaria o esterna e di aggiungere colonne alla tabella.

#### AGGIUNGI O RILASCIA VINCOLO

Le seguenti query SQL mostrano esempi di aggiunta o rilascio di vincoli a una tabella.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parametri**

- `table_name`: Nome della tabella che si sta modificando.
- `constraint_name`: Nome del vincolo che si desidera aggiungere o eliminare.
- `column_name`: Nome della colonna a cui si sta aggiungendo un vincolo.
- `referenced_table_name`: Nome della tabella a cui fa riferimento la chiave esterna.
- `primary_column_name`: Nome della colonna a cui fa riferimento la chiave esterna.

>[!NOTE]
>
>Lo schema della tabella deve essere univoco e non deve essere condiviso tra più tabelle. Inoltre, lo spazio dei nomi è obbligatorio per i vincoli di chiave primaria.

#### AGGIUNGI COLONNA

Le seguenti query SQL mostrano esempi di aggiunta di colonne a una tabella.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parametri**

- `table_name`: Nome della tabella che si sta modificando.
- `column_name`: Nome della colonna da aggiungere.
- `data_type`: Il tipo di dati della colonna da aggiungere. I tipi di dati supportati includono: bigint, char, stringa, data, datetime, doppio, precisione doppia, numero intero, piccolo, tinyint, varchar.

### MOSTRA CHIAVI PRINCIPALI

Il comando `SHOW PRIMARY KEYS` elenca tutti i vincoli di chiave primaria per il database specificato.

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

Il comando `SHOW FOREIGN KEYS` elenca tutti i vincoli di chiave esterna per il database specificato.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
