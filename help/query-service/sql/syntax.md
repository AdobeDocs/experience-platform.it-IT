---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;sintassi SQL;sql;ctas;CTAS;Creare una tabella come selezionato'
solution: Experience Platform
title: Sintassi SQL
topic: syntax
description: Questo documento mostra la sintassi SQL supportata da Query Service.
translation-type: tm+mt
source-git-commit: 14cb1d304fd8aad2ca287f8d66ac6865425db4c5
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 0%

---


# Sintassi SQL

[!DNL Query Service] consente di utilizzare SQL ANSI standard per  `SELECT` istruzioni e altri comandi limitati. Questo documento mostra la sintassi SQL supportata da [!DNL Query Service].

## Definire una query SELECT

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

dove `from_item` può essere uno dei seguenti:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

e `grouping_element` può essere:

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

e `with_query` è:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### Clausola SNAPSHOT

Questa clausola può essere utilizzata per leggere i dati in una tabella in modo incrementale in base agli ID snapshot. Un ID snapshot è un indicatore del punto di controllo identificato da un numero, di tipo Long, su una tabella data-ake ogni volta che vi vengono scritti dati. La clausola SNAPSHOT si collega alla relazione della tabella utilizzata accanto a essa.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Esempio

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Una clausola SNAPSHOT funziona con un alias di tabella o di tabella, ma non sopra una sottoquery o una visualizzazione. Una clausola SNAPHOST funzionerà ovunque sia possibile applicare una query SELECT su una tabella.

### Clausola WHERE ILIKE

La parola chiave ILIKE può essere utilizzata invece di LIKE per effettuare corrispondenze sulla clausola WHERE della query SELECT senza distinzione tra maiuscole e minuscole.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

La logica delle clausole LIKE e ILIKE è la seguente:
- ```WHERE condition LIKE pattern```,  ```~~``` equivale a un pattern
- ```WHERE condition NOT LIKE pattern```,  ```!~~``` equivale a un pattern
- ```WHERE condition ILIKE pattern```,  ```~~*``` equivalente al pattern
- ```WHERE condition NOT ILIKE pattern```,  ```!~~*``` equivalente al pattern


#### Esempio

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Restituisce i clienti con nomi che iniziano in &quot;A&quot; o &quot;a&quot;.

## JOINS

Una query `SELECT` con join ha la sintassi seguente:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNIONE, INTERSECT ed ECCETTO

Le clausole `UNION`, `INTERSECT` e `EXCEPT` sono supportate per combinare o escludere righe simili da due o più tabelle:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CREA TABELLA COME SELEZIONATA

La sintassi seguente definisce una query `CREATE TABLE AS SELECT` (CTAS) supportata da [!DNL Query Service]:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

dove
`target_schema_title` è il titolo dello schema XDM. Utilizzare questa clausola solo se si desidera utilizzare uno schema XDM esistente per il nuovo dataset creato dalla query CTAS
`rowvalidation` specifica se l&#39;utente desidera la convalida a livello di riga di ogni nuovo batch acquisito per il nuovo set di dati creato. Il valore predefinito è &#39;true&#39;

e `select_query` è un&#39;istruzione `SELECT` la cui sintassi è definita sopra in questo documento.


### Esempio

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Si prega di notare che per una data query CTAS:

1. L&#39;istruzione `SELECT` deve avere un alias per le funzioni di aggregazione come `COUNT`, `SUM`, `MIN` e così via.
2. L&#39;istruzione `SELECT` può essere fornita con o senza parentesi ().
3. L&#39;istruzione `SELECT` può essere fornita con una clausola SNAPSHOT per leggere i delta incrementali nella tabella di destinazione.

```sql
CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

## INSERISCI IN

La sintassi seguente definisce una query `INSERT INTO` supportata da [!DNL Query Service]:

```sql
INSERT INTO table_name select_query
```

dove `select_query` è un&#39;istruzione `SELECT` la cui sintassi è definita sopra in questo documento.

### Esempio

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Si noti che per una data query INSERT INTO:

1. L&#39;istruzione `SELECT` NON DEVE essere racchiusa tra parentesi ().
2. Lo schema del risultato dell&#39;istruzione `SELECT` deve essere conforme a quello della tabella definita nell&#39;istruzione `INSERT INTO`.
3. L&#39;istruzione `SELECT` può essere fornita con una clausola SNAPSHOT per leggere i delta incrementali nella tabella di destinazione.

```sql
INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

### TABELLA DI RILASCIO

Eliminare una tabella ed eliminare la directory associata alla tabella dal file system se non si tratta di una tabella ESTERNA. Se la tabella da eliminare non esiste, si verifica un&#39;eccezione.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parametri

- `IF EXISTS`: Se la tabella non esiste, non si verifica nulla
- `TEMP`: Tabella temporanea

## CREA VISUALIZZAZIONE

La sintassi seguente definisce una query `CREATE VIEW` supportata da [!DNL Query Service]:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Dove `view_name` è il nome della visualizzazione da creare
e `select_query` è un&#39;istruzione `SELECT` la cui sintassi è definita sopra in questo documento.

Esempio:

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### VISUALIZZAZIONE A DISCESA

La sintassi seguente definisce una query `DROP VIEW` supportata da [!DNL Query Service]:

```sql
DROP VIEW [IF EXISTS] view_name
```

Dove `view_name` è il nome della visualizzazione da eliminare

Esempio:

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] Comandi SQL

### SET

Impostare una proprietà, restituire il valore di una proprietà esistente o elencare tutte le proprietà esistenti. Se viene fornito un valore per una chiave di proprietà esistente, il valore precedente viene ignorato.

```sql
SET property_key [ To | =] property_value
```

Per restituire il valore per qualsiasi impostazione, utilizzare `SHOW [setting name]`.

## Comandi PostgreSQL

### INIZIO

Questo comando viene analizzato e il comando completato viene inviato nuovamente al client. È lo stesso del comando `START TRANSACTION`.

```sql
BEGIN [ TRANSACTION ]
```

#### Parametri

- `TRANSACTION`: Parole chiave facoltative. La ascolta, non viene eseguita alcuna azione.

### CHIUDI

`CLOSE` libera le risorse associate a un cursore aperto. Dopo la chiusura del cursore, non sono consentite operazioni successive. Un cursore deve essere chiuso quando non è più necessario.

```sql
CLOSE { name }
```

#### Parametri

- `name`: il nome di un cursore aperto da chiudere.

### COMMIT

Nessuna azione viene eseguita in [!DNL Query Service] come risposta all&#39;istruzione della transazione di commit.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### Parametri

- `WORK`
- `TRANSACTION`: Parole chiave facoltative. Non hanno effetto.

### DEALLOCATE

Utilizzare `DEALLOCATE` per deallocare un&#39;istruzione SQL precedentemente preparata. Se non si dealloca in modo esplicito un&#39;istruzione preparata, questa viene deallocata al termine della sessione.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parametri

- `Prepare`: Questa parola chiave viene ignorata.
- `name`: Il nome dell&#39;istruzione preparata da deallocare.
- `ALL`: Disallocare tutte le istruzioni preparate.

### DICHIARARE

`DECLARE` consente all&#39;utente di creare cursori, che possono essere utilizzati per recuperare un numero limitato di righe alla volta da una query più grande. Una volta creato il cursore, le righe vengono recuperate da esso utilizzando `FETCH`.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parametri

- `name`: Nome del cursore da creare.
- `WITH HOLD`: Specifica che il cursore può continuare a essere utilizzato dopo che la transazione che l&#39;ha creato ha avuto esito positivo.
- `query`: Un  `SELECT` comando  `VALUES` o che fornisce le righe che devono essere restituite dal cursore.

### ESECUZIONE

`EXECUTE` viene utilizzata per eseguire un&#39;istruzione preparata in precedenza. Poiché le istruzioni preparate esistono solo per la durata di una sessione, l&#39;istruzione preparata deve essere stata creata da un&#39;istruzione `PREPARE` eseguita in precedenza nella sessione corrente.

Se l&#39;istruzione `PREPARE` che ha creato l&#39;istruzione ha specificato alcuni parametri, è necessario trasmettere un insieme compatibile di parametri all&#39;istruzione `EXECUTE`, altrimenti viene generato un errore. Tenere presente che le istruzioni preparate (a differenza delle funzioni) non vengono sovraccaricate in base al tipo o al numero dei relativi parametri. Il nome di un&#39;istruzione preparata deve essere univoco all&#39;interno di una sessione del database.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parametri

- `name`: Nome dell&#39;istruzione preparata da eseguire.
- `parameter`: Il valore effettivo di un parametro per l&#39;istruzione preparata. Deve essere un&#39;espressione che genera un valore compatibile con il tipo di dati di questo parametro, come determinato al momento della creazione dell&#39;istruzione preparata.

### SPIEGARE

Questo comando visualizza il piano di esecuzione generato dal planner PostgreSQL per l&#39;istruzione fornita. Il piano di esecuzione mostra come verranno analizzate le tabelle a cui fa riferimento l&#39;istruzione — mediante scansione sequenziale normale, scansione indice e così via — e se si fa riferimento a più tabelle, quali algoritmi di join vengono utilizzati per riunire le righe richieste da ogni tabella di input.

La parte più critica del display è il costo stimato di esecuzione del rendiconto, che è la stima del planner in base al tempo necessario per eseguire l&#39;istruzione (misurato in unità di costo arbitrarie, ma tradizionalmente medie del recupero di pagine disco). In realtà, vengono visualizzati due numeri: il costo iniziale prima della prima riga può essere restituito e il costo totale per restituire tutte le righe. Per la maggior parte delle query, il costo totale è ciò che conta, ma in contesti come una sottoquery in EXISTS, il planner sceglie il costo iniziale più piccolo invece del costo totale più piccolo (perché l&#39;esecutore si ferma dopo aver ottenuto una riga, comunque). Inoltre, se si limita il numero di righe da restituire con una clausola `LIMIT`, il planner effettua un&#39;interpolazione appropriata tra i costi dell&#39;endpoint per stimare quale piano è effettivamente il più economico.

L&#39;opzione `ANALYZE` determina l&#39;esecuzione dell&#39;istruzione, non solo pianificata. Quindi, vengono aggiunte statistiche sul tempo di esecuzione effettivo, compreso il tempo totale trascorso all&#39;interno di ciascun nodo del piano (in millisecondi) e il numero totale di righe che ha restituito. Questo è utile per vedere se le stime dell&#39;urbanista sono vicine alla realtà.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parametri

- `ANALYZE`: Eseguire il comando e visualizzare i tempi di esecuzione effettivi e altre statistiche. Il valore predefinito di questo parametro è `FALSE`.
- `FORMAT`: Specificate il formato di output, che può essere TEXT, XML, JSON o YAML. L&#39;output non testuale contiene le stesse informazioni del formato di output del testo, ma è più semplice da analizzare per i programmi. Il valore predefinito di questo parametro è `TEXT`.
- `statement`: Qualsiasi  `SELECT`,  `INSERT`,  `UPDATE`,  `DELETE`,  `VALUES`,  `EXECUTE`,  `DECLARE`,  `CREATE TABLE AS`o  `CREATE MATERIALIZED VIEW AS` istruzione di cui si desidera visualizzare il piano di esecuzione.

>[!IMPORTANT]
>
>Tenere presente che l&#39;istruzione viene effettivamente eseguita quando si utilizza l&#39;opzione `ANALYZE`. Sebbene `EXPLAIN` scarti qualsiasi output restituito da un `SELECT`, altri effetti collaterali dell&#39;istruzione si verificano normalmente.

#### Esempio

Per visualizzare il piano per una semplice query su una tabella con una singola `integer` colonna e 10000 righe:

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` recupera le righe utilizzando un cursore creato in precedenza.

A un cursore è associata una posizione, che viene utilizzata da `FETCH`. La posizione del cursore può essere prima della prima riga del risultato della query, su una riga specifica del risultato o dopo l&#39;ultima riga del risultato. Quando viene creato, un cursore viene posizionato prima della prima riga. Dopo aver recuperato alcune righe, il cursore viene posizionato sulla riga recuperata più di recente. Se `FETCH` viene eseguito al di fuori della fine delle righe disponibili, il cursore viene posizionato a sinistra dopo l&#39;ultima riga. In assenza di tale riga, viene restituito un risultato vuoto e i cursori vengono posizionati prima della prima riga o dopo l&#39;ultima riga, a seconda dei casi.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parametri

- `num_of_rows`: Una costante integer con segno che può determinare la posizione o il numero di righe da recuperare.
- `cursor_name`: Nome di un cursore aperto.

### PREPARARE

`PREPARE` crea un&#39;istruzione preparata. Un&#39;istruzione preparata è un oggetto lato server che può essere utilizzato per ottimizzare le prestazioni. Quando l&#39;istruzione `PREPARE` viene eseguita, l&#39;istruzione specificata viene analizzata, analizzata e riscritta. Quando viene emesso un comando `EXECUTE`, l&#39;istruzione preparata viene pianificata ed eseguita. Questa divisione del lavoro evita il lavoro ripetitivo di analisi parse, consentendo al piano di esecuzione di dipendere dai valori specifici dei parametri forniti.

Le istruzioni preparate possono accettare parametri, valori che vengono sostituiti nell&#39;istruzione quando viene eseguita. Durante la creazione dell&#39;istruzione preparata, fare riferimento ai parametri per posizione, utilizzando $1, $2 e così via. Facoltativamente, è possibile specificare un elenco corrispondente di tipi di dati di parametro. Se il tipo di dati di un parametro non è specificato o è dichiarato sconosciuto, il tipo viene ricavato dal contesto in cui il parametro viene fatto riferimento per la prima volta, se possibile. Durante l&#39;esecuzione dell&#39;istruzione, specificare i valori effettivi di questi parametri nell&#39;istruzione `EXECUTE`.

Le istruzioni preparate durano solo per la durata della sessione corrente del database. Al termine della sessione, l&#39;istruzione preparata viene dimenticata, pertanto deve essere ricreata prima di essere riutilizzata. Ciò significa anche che una singola istruzione preparata non può essere utilizzata da più client di database simultanei. Tuttavia, ogni client può creare una propria istruzione preparata da utilizzare. Le istruzioni preparate possono essere pulite manualmente utilizzando il comando `DEALLOCATE`.

Le istruzioni preparate possono potenzialmente avere il maggiore vantaggio in termini di prestazioni quando una singola sessione viene utilizzata per eseguire un numero elevato di istruzioni simili. La differenza di prestazioni è particolarmente significativa se le istruzioni sono complesse da pianificare o riscrivere, ad esempio se la query include un join di molte tabelle o richiede l&#39;applicazione di più regole. Se l&#39;istruzione è relativamente semplice da pianificare e riscrivere ma relativamente costoso da eseguire, il vantaggio di prestazioni delle istruzioni preparate è meno evidente.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parametri

- `name`: Un nome arbitrario assegnato a questa particolare istruzione preparata. Deve essere univoco all&#39;interno di una singola sessione e successivamente viene utilizzato per eseguire o deallocare un&#39;istruzione preparata in precedenza.
- `data-type`: Il tipo di dati di un parametro per l&#39;istruzione preparata. Se il tipo di dati di un particolare parametro non è specificato o è specificato come sconosciuto, viene ricavato dal contesto in cui viene fatto primo riferimento al parametro. Per fare riferimento ai parametri dell&#39;istruzione preparata, utilizzare $1, $2 e così via.


### ROLLBACK

`ROLLBACK` esegue il rollback della transazione corrente e causa l&#39;eliminazione di tutti gli aggiornamenti effettuati dalla transazione.

```sql
ROLLBACK [ WORK ]
```

#### Parametri

- `WORK`

### SELEZIONA IN

`SELECT INTO` crea una nuova tabella e la riempie con i dati calcolati da una query. I dati non vengono restituiti al client, come avviene con un `SELECT` normale. Alle colonne della nuova tabella sono associati i nomi e i tipi di dati alle colonne di output della `SELECT`.

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

#### Parametri

- `TEMPORARAY` o  `TEMP`: Se specificato, la tabella viene creata come tabella temporanea.
- `UNLOGGED:` se specificato, la tabella viene creata come tabella non registrata.
- `new_table` Nome (eventualmente qualificato per lo schema) della tabella da creare.

#### Esempio

Creare una nuova tabella `films_recent` costituita esclusivamente da voci recenti della tabella `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRA

`SHOW` visualizza l&#39;impostazione corrente dei parametri di esecuzione. Queste variabili possono essere impostate utilizzando l&#39;istruzione `SET`, modificando il file di configurazione postgresql.conf, tramite la variabile ambientale `PGOPTIONS` (quando si utilizza libpq o un&#39;applicazione basata su libpq), o tramite i flag della riga di comando all&#39;avvio del server postgres.

```sql
SHOW name
```

#### Parametri

- `name`
   - `SERVER_VERSION`: Mostra il numero di versione del server.
   - `SERVER_ENCODING`: Mostra la codifica del set di caratteri lato server. Al momento, questo parametro può essere mostrato ma non impostato, perché la codifica è determinata al momento della creazione del database.
   - `LC_COLLATE`: Mostra le impostazioni internazionali del database per le regole di confronto (ordine del testo). Al momento, questo parametro può essere mostrato ma non impostato, perché l&#39;impostazione è determinata al momento della creazione del database.
   - `LC_CTYPE`: Mostra le impostazioni internazionali del database per la classificazione dei caratteri. Al momento, questo parametro può essere mostrato ma non impostato, perché l&#39;impostazione è determinata al momento della creazione del database.
      `IS_SUPERUSER`: True se il ruolo corrente dispone di privilegi di superutente.
- `ALL`: Mostra i valori di tutti i parametri di configurazione con le descrizioni.

#### Esempio

Mostra l&#39;impostazione corrente del parametro `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### AVVIA TRANSAZIONE

Questo comando viene analizzato e invia di nuovo il comando completato al client. È lo stesso del comando `BEGIN`.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### COPY

Questo comando scarica l&#39;output di qualsiasi query SELECT in una posizione specificata. Affinché il comando abbia esito positivo, l&#39;utente deve avere accesso a questa posizione.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>Il percorso di output completo sarà `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTER

Questo comando consente di aggiungere o eliminare vincoli di chiave primaria o esterna nella tabella.

```sql
Alter TABLE table_name ADD CONSTRAINT Primary key ( column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name ( primary_column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name Namespace 'namespace'

Alter TABLE table_name DROP CONSTRAINT Primary key ( column_name )

Alter TABLE table_name DROP CONSTRAINT  Foreign key ( column_name )
```

>[!NOTE]
>Lo schema di tabella deve essere univoco e non deve essere condiviso tra più tabelle. Inoltre, lo spazio nomi è obbligatorio.


### MOSTRA TASTI PRINCIPALI

Questo comando elenca tutti i vincoli di chiave primaria per il database specificato.

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### MOSTRA TASTI ESTERNI

Questo comando elenca tutti i vincoli di chiave esterna per il database specificato.

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
