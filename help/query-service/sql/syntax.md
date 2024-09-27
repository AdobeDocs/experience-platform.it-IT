---
keywords: Experience Platform;home;argomenti comuni;servizio query;servizio query;sintassi SQL;sql;ctas;CTAS;Crea tabella come selezione
solution: Experience Platform
title: Sintassi SQL in Query Service
description: Questo documento descrive e spiega la sintassi SQL supportata da Adobe Experience Platform Query Service.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '4291'
ht-degree: 2%

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

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN HEAD AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND TAIL;

SELECT * FROM (SELECT id FROM table_to_be_queried BETWEEN start_snapshot_id AND end_snapshot_id) C 

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

Nella tabella seguente viene illustrato il significato di ogni opzione di sintassi all&#39;interno della clausola SNAPSHOT.

| Sintassi | Significato |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Legge i dati a partire dall&#39;ID snapshot specificato (esclusivo). |
| `AS OF end_snapshot_id` | Legge i dati così come si trovavano nell’ID snapshot specificato (incluso). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Legge i dati tra gli ID snapshot iniziale e finale specificati. È esclusivo di `start_snapshot_id` e include `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | Legge i dati dall&#39;inizio (prima del primo snapshot) all&#39;ID snapshot iniziale specificato (incluso). Si noti che questa opzione restituisce solo righe in `start_snapshot_id`. |
| `BETWEEN end_snapshot_id AND TAIL` | Legge i dati da subito dopo il `end-snapshot_id` specificato alla fine del set di dati (escluso l&#39;ID snapshot). Ciò significa che se `end_snapshot_id` è l&#39;ultimo snapshot nel set di dati, la query restituirà zero righe perché non sono presenti snapshot oltre l&#39;ultimo snapshot. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Legge i dati a partire dall&#39;ID snapshot specificato da `table_to_be_queried` e li unisce ai dati da `table_to_be_joined` come in `your_chosen_snapshot_id`. Il join si basa sugli ID corrispondenti delle colonne ID delle due tabelle unite in join. |

Una clausola `SNAPSHOT` funziona con un alias di tabella o tabella ma non sopra una sottoquery o vista. Una clausola `SNAPSHOT` funziona ovunque sia possibile applicare una query `SELECT` su una tabella.

È inoltre possibile utilizzare `HEAD` e `TAIL` come valori di offset speciali per le clausole snapshot. L&#39;utilizzo di `HEAD` fa riferimento a un offset prima del primo snapshot, mentre `TAIL` fa riferimento a un offset dopo l&#39;ultimo snapshot.

>[!NOTE]
>
>Se si esegue una query tra due ID snapshot, possono verificarsi i due scenari seguenti se lo snapshot iniziale è scaduto e il flag di comportamento di fallback facoltativo (`resolve_fallback_snapshot_on_failure`) è impostato:
>
>- Se è impostato il flag di comportamento di fallback facoltativo, Query Service sceglie lo snapshot disponibile più recente, lo imposta come snapshot iniziale e restituisce i dati tra lo snapshot disponibile più recente e quello finale specificato. Questi dati sono **inclusivi** della prima istantanea disponibile.

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

La sintassi seguente definisce una query `CREATE TABLE AS SELECT` (CTAS):

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| Elemento “parameters” | Descrizione |
| ----- | ----- |
| `schema` | Titolo dello schema XDM. Utilizzare questa clausola solo se si desidera utilizzare uno schema XDM esistente per il nuovo set di dati creato dalla query CTAS. |
| `rowvalidation` | (Facoltativo) Specifica se l’utente desidera la convalida a livello di riga di ogni nuovo batch acquisito per il set di dati appena creato. Il valore predefinito è `true`. |
| `label` | Quando crei un set di dati con una query CTAS, utilizza questa etichetta con il valore di `profile` per etichettare il set di dati come abilitato per il profilo. Ciò significa che il set di dati viene automaticamente contrassegnato per il profilo durante la creazione. Per ulteriori informazioni sull&#39;utilizzo di `label`, vedere il documento dell&#39;estensione dell&#39;attributo derivato. |
| `select_query` | Un&#39;istruzione `SELECT`. La sintassi della query `SELECT` si trova nella sezione [SELECT queries](#select-queries). |

**Esempio**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>L&#39;istruzione `SELECT` deve avere un alias per le funzioni di aggregazione come `COUNT`, `SUM`, `MIN` e così via. Inoltre, l&#39;istruzione `SELECT` può essere fornita con o senza parentesi (). È possibile fornire una clausola `SNAPSHOT` per leggere i delta incrementali nella tabella di destinazione.

## INSERISCI IN

Il comando `INSERT INTO` è definito come segue:

```sql
INSERT INTO table_name select_query
```

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `IF EXISTS` | Se specificato, non viene generata alcuna eccezione se il database **non** esiste. |

## ELIMINA SCHEMA

Il comando `DROP SCHEMA` elimina uno schema esistente.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
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
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## VISTA A DISCESA

La sintassi seguente definisce una query `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Elemento “parameters” | Descrizione |
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
      WHEN OTHER
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
  WHEN OTHER THEN
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
EXCEPTION WHEN OTHER THEN 
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
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Dopo aver impostato il flag `auto_to_json`

Nella tabella seguente viene illustrata la differenza di risultati dell&#39;impostazione `auto_to_json` nel set di dati risultante. In entrambi gli scenari è stata utilizzata la stessa query SELECT.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Risolvi snapshot di fallback in caso di errore {#resolve-fallback-snapshot-on-failure}

L&#39;opzione `resolve_fallback_snapshot_on_failure` viene utilizzata per risolvere il problema di un ID di snapshot scaduto. I metadati dello snapshot scadono dopo due giorni e uno snapshot scaduto può invalidare la logica di uno script. Questo problema può verificarsi quando si utilizzano blocchi anonimi.

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
  WHEN OTHER THEN
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
WHEN other THEN SELECT 'ERROR';

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

| SKU (Stock Keeping Unit) | _experience | quantità | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;) | 5 | 10,5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;)) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)) | 3 | 12 |

## IMPOSTA

Il comando `SET` imposta una proprietà e restituisce il valore di una proprietà esistente oppure elenca tutte le proprietà esistenti. Se viene fornito un valore per una chiave di proprietà esistente, il valore precedente viene sovrascritto.

```sql
SET property_key = property_value
```

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `property_key` | Nome della proprietà che si desidera elencare o modificare. |
| `property_value` | Il valore con cui si desidera impostare la proprietà. |

Per restituire il valore per qualsiasi impostazione, utilizzare `SET [property key]` senza `property_value`.

## [!DNL PostgreSQL] comandi

Le sottosezioni seguenti descrivono i comandi [!DNL PostgreSQL] supportati da Query Service.

### ANALIZZARE LA TABELLA {#analyze-table}

Il comando `ANALYZE TABLE` esegue un&#39;analisi di distribuzione e calcoli statistici per la tabella o le tabelle denominate. L&#39;utilizzo di `ANALYZE TABLE` varia a seconda che i set di dati siano archiviati nell&#39;[archivio accelerato](#compute-statistics-accelerated-store) o nel [data lake](#compute-statistics-data-lake). Per ulteriori informazioni sull’uso di questa variabile, consulta le rispettive sezioni.

#### STATISTICHE DI CALCOLO sull&#39;archivio accelerato {#compute-statistics-accelerated-store}

Il comando `ANALYZE TABLE` calcola le statistiche per una tabella nell&#39;archivio accelerato. Le statistiche sono calcolate sulle query CTAS o ITAS eseguite per una determinata tabella nell’archivio accelerato.

**Esempio**

```sql
ANALYZE TABLE <original_table_name>
```

Di seguito è riportato un elenco dei calcoli statistici disponibili dopo l&#39;utilizzo del comando `ANALYZE TABLE`:-

| Valori calcolati | Descrizione |
|---|---|
| `field` | Nome della colonna in una tabella. |
| `data-type` | Tipo di dati accettabile per ogni colonna. |
| `count` | Numero di righe contenenti un valore non nullo per questo campo. |
| `distinct-count` | Il numero di valori univoci o distinti per questo campo. |
| `missing` | Numero di righe con valore Null per questo campo. |
| `max` | Valore massimo della tabella analizzata. |
| `min` | Valore minimo della tabella analizzata. |
| `mean` | Valore medio della tabella analizzata. |
| `stdev` | Deviazione standard della tabella analizzata. |

#### STATISTICHE DI CALCOLO sul data lake {#compute-statistics-data-lake}

È ora possibile calcolare le statistiche a livello di colonna sui set di dati [!DNL Azure Data Lake Storage] (ADLS) con il comando SQL `COMPUTE STATISTICS`. Calcola le statistiche delle colonne sull’intero set di dati, su un sottoinsieme di un set di dati, su tutte le colonne o su un sottoinsieme di colonne.

`COMPUTE STATISTICS` estende il comando `ANALYZE TABLE`. Tuttavia, i comandi `COMPUTE STATISTICS`, `FILTERCONTEXT` e `FOR COLUMNS` non sono supportati nelle tabelle di archivio accelerate. Queste estensioni per il comando `ANALYZE TABLE` sono attualmente supportate solo per le tabelle ADLS.

**Esempio**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

Il comando `FILTER CONTEXT` calcola le statistiche su un sottoinsieme del set di dati in base alla condizione del filtro fornita. Il comando `FOR COLUMNS` esegue il targeting di colonne specifiche per l&#39;analisi.

>[!NOTE]
>
>`Statistics ID` e le statistiche generate sono valide solo per ogni sessione e non è possibile accedervi in diverse sessioni PSQL.<br><br>Limitazioni:<ul><li>La generazione di statistiche non è supportata per i tipi di dati array o mappa</li><li>Le statistiche calcolate sono **non** persistenti tra sessioni diverse.</li></ul><br><br>Opzioni:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>Per impostazione predefinita, il flag è impostato su true. Di conseguenza, quando le statistiche vengono richieste su un tipo di dati non supportato, non viene generato un errore ma i campi vengono ignorati automaticamente con i tipi di dati non supportati.<br>Per abilitare le notifiche sugli errori quando vengono richieste statistiche su un tipo di dati non supportato, utilizzare: `SET skip_stats_for_complex_datatypes = false`.

L’output della console viene visualizzato come illustrato di seguito.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

È quindi possibile eseguire direttamente una query sulle statistiche calcolate facendo riferimento a `Statistics ID`. Utilizzare `Statistics ID` o il nome dell&#39;alias come illustrato nell&#39;istruzione di esempio seguente per visualizzare l&#39;output completo. Per ulteriori informazioni su questa funzione, consulta la [documentazione sul nome alias](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Utilizzare il comando `SHOW STATISTICS` per visualizzare i metadati per tutte le statistiche temporanee generate nella sessione. Questo comando consente di perfezionare l’ambito dell’analisi statistica.

```sql
SHOW STATISTICS;
```

Di seguito è riportato un esempio di output di SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Per ulteriori informazioni, consulta la [documentazione sulle statistiche del set di dati](../key-concepts/dataset-statistics.md).

#### TABELLAMPIO {#tablesample}

Adobe Experience Platform Query Service fornisce set di dati di esempio come parte delle sue funzionalità di elaborazione delle query approssimative.

È consigliabile utilizzare gli esempi di set di dati quando non è necessaria una risposta esatta per un’operazione di aggregazione su un set di dati. Per eseguire query esplorative più efficienti su set di dati di grandi dimensioni tramite una query approssimativa per restituire una risposta approssimativa, utilizzare la funzionalità `TABLESAMPLE`.

I set di dati di esempio vengono creati con campioni casuali uniformi dai set di dati esistenti [!DNL Azure Data Lake Storage] (ADLS), utilizzando solo una percentuale di record dell&#39;originale. La funzionalità di esempio del set di dati estende il comando `ANALYZE TABLE` con i comandi SQL `TABLESAMPLE` e `SAMPLERATE`.

Nell’esempio seguente, la riga 1 illustra come calcolare un campione del 5% della tabella. La riga 2 illustra come calcolare un campione del 5% da una visualizzazione filtrata dei dati all’interno della tabella.

**Esempio**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Per ulteriori informazioni, consulta la [documentazione sugli esempi di set di dati](../key-concepts/dataset-samples.md).

### INIZIO

Il comando `BEGIN` o, in alternativa, il comando `BEGIN WORK` o `BEGIN TRANSACTION`, avvia un blocco della transazione. Tutte le istruzioni immesse dopo il comando begin verranno eseguite in una singola transazione fino a quando non viene fornito un comando COMMIT o ROLLBACK esplicito. Comando uguale a `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CHIUDI

Il comando `CLOSE` libera le risorse associate a un cursore aperto. Dopo la chiusura del cursore non sono consentite operazioni successive. Quando il cursore non è più necessario, è necessario chiuderlo.

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

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `name` | Nome del cursore da creare. |
| `query` | Comando `SELECT` o `VALUES` che fornisce le righe che devono essere restituite dal cursore. |

### ESEGUI

Il comando `EXECUTE` viene utilizzato per eseguire un&#39;istruzione preparata in precedenza. Poiché le istruzioni preparate esistono solo durante una sessione, l&#39;istruzione preparata deve essere stata creata da un&#39;istruzione `PREPARE` eseguita in precedenza nella sessione corrente. Ulteriori informazioni sull&#39;utilizzo delle istruzioni preparate sono disponibili nella sezione [`PREPARE` comando](#prepare).

Se l&#39;istruzione `PREPARE` che ha creato l&#39;istruzione ha specificato alcuni parametri, è necessario passare un set di parametri compatibile all&#39;istruzione `EXECUTE`. Se questi parametri non vengono passati, viene generato un errore.

```sql
EXECUTE name [ ( parameter ) ]
```

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
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
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### RECUPERA

Il comando `FETCH` recupera le righe utilizzando un cursore creato in precedenza.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `name` | Nome dell&#39;istruzione preparata. |
| `data_type` | I tipi di dati dei parametri dell&#39;istruzione preparata. Se il tipo di dati di un parametro non è elencato, è possibile dedurlo dal contesto. Se devi aggiungere più tipi di dati, puoi aggiungerli in un elenco separato da virgole. |

### ROLLBACK

Il comando `ROLLBACK` annulla la transazione corrente ed elimina tutti gli aggiornamenti effettuati dalla transazione.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELEZIONA IN

Il comando `SELECT INTO` crea una nuova tabella e la riempie con i dati calcolati da una query. I dati non vengono restituiti al client, come avviene con un normale comando `SELECT`. Le colonne della nuova tabella hanno i nomi e i tipi di dati associati alle colonne di output del comando `SELECT`.

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

Ulteriori informazioni sui parametri di query SELECT standard sono disponibili nella [sezione di query SELECT](#select-queries). In questa sezione sono elencati solo i parametri esclusivi del comando `SELECT INTO`.

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `TEMPORARY` o `TEMP` | Un parametro facoltativo. Se il parametro è specificato, la tabella creata è una tabella temporanea. |
| `UNLOGGED` | Un parametro facoltativo. Se si specifica il parametro, la tabella creata è una tabella non registrata. Ulteriori informazioni sulle tabelle non registrate sono disponibili nella [[!DNL PostgreSQL] documentazione](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Nome della tabella da creare. |

**Esempio**

La query seguente crea una nuova tabella `films_recent` costituita solo da voci recenti della tabella `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### MOSTRA

Il comando `SHOW` visualizza l&#39;impostazione corrente dei parametri di runtime. Queste variabili possono essere impostate utilizzando l&#39;istruzione `SET`, modificando il file di configurazione `postgresql.conf`, tramite la variabile di ambiente `PGOPTIONS` (quando si utilizza libpq o un&#39;applicazione basata su libpq) o tramite i flag della riga di comando all&#39;avvio del server Postgres.

```sql
SHOW name
SHOW ALL
```

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `name` | Nome del parametro di runtime di cui si desidera ottenere informazioni. I valori possibili per il parametro runtime includono i seguenti valori:<br>`SERVER_VERSION`: questo parametro mostra il numero di versione del server.<br>`SERVER_ENCODING`: questo parametro mostra la codifica del set di caratteri lato server.<br>`LC_COLLATE`: questo parametro mostra l&#39;impostazione delle impostazioni locali del database per le regole di confronto (ordinamento testo).<br>`LC_CTYPE`: questo parametro mostra l&#39;impostazione delle impostazioni locali del database per la classificazione dei caratteri.<br>`IS_SUPERUSER`: questo parametro indica se il ruolo corrente dispone di privilegi di utente avanzato. |
| `ALL` | Mostra i valori di tutti i parametri di configurazione con le relative descrizioni. |

**Esempio**

La query seguente mostra l&#39;impostazione corrente del parametro `DateStyle`.

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

Il comando `COPY` duplica l&#39;output di qualsiasi query `SELECT` in un percorso specificato. Affinché il comando venga eseguito correttamente, l&#39;utente deve avere accesso a questa posizione.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Elemento “parameters” | Descrizione |
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

| Elemento “parameters” | Descrizione |
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

Gli esempi seguenti aggiungono un’identità primaria e un’identità secondaria aggiungendo vincoli.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Le identità possono anche essere rimosse eliminando i vincoli, come mostrato nell’esempio seguente.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Per informazioni più dettagliate, consulta il documento su [impostazione di identità in set di dati ad hoc](../data-governance/ad-hoc-schema-identities.md).

#### AGGIUNGI COLONNA

Le query SQL seguenti mostrano esempi di aggiunta di colonne a una tabella.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Tipi di dati supportati

Nella tabella seguente sono elencati i tipi di dati accettati per l&#39;aggiunta di colonne a una tabella con [!DNL Postgres SQL], XDM e [!DNL Accelerated Database Recovery] (ADR) in SQL di Azure.

| — | Client PSQL | XDM | ADR | Descrizione |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Tipo di dati numerico utilizzato per memorizzare numeri interi di grandi dimensioni compresi tra -9.223.372.036.854.775.807 e 9.223.372.036.854.775.807 in 8 byte. |
| 2 | `integer` | `int4` | `integer` | Tipo di dati numerico utilizzato per memorizzare numeri interi compresi tra -2.147.483.648 e 2.147.483.647 in 4 byte. |
| 3 | `smallint` | `int2` | `smallint` | Tipo di dati numerici utilizzato per memorizzare numeri interi compresi tra -32.768 e 215-1 32.767 in 2 byte. |
| 4 | `tinyint` | `int1` | `tinyint` | Tipo di dati numerico utilizzato per memorizzare valori interi compresi tra 0 e 255 in 1 byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Tipo di dati carattere di dimensioni variabili. È consigliabile utilizzare `varchar` quando le dimensioni delle voci di dati della colonna variano notevolmente. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` e `FLOAT` sono sinonimo validi per `DOUBLE PRECISION`. `double precision` è un tipo di dati a virgola mobile. I valori a virgola mobile sono memorizzati in 8 byte. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` è un sinonimo valido per `double precision`.`double precision` è un tipo di dati a virgola mobile. I valori a virgola mobile sono memorizzati in 8 byte. |
| 8 | `date` | `date` | `date` | I tipi di dati `date` sono valori di data di calendario memorizzati a 4 byte senza informazioni di marca temporale. L’intervallo di date valide è compreso tra 01-01-0001 e 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Tipo di dati utilizzato per memorizzare un istante di tempo espresso come data e ora del calendario. `datetime` include i qualificatori di: anno, mese, giorno, ora, secondo e frazione. Una dichiarazione `datetime` può includere qualsiasi sottoinsieme di queste unità di tempo che sono unite in quella sequenza o che comprendono solo una singola unità di tempo. |
| 10 | `char(len)` | `string` | `char(len)` | La parola chiave `char(len)` viene utilizzata per indicare che l&#39;elemento è un carattere a lunghezza fissa. |

#### AGGIUNGI SCHEMA

La query SQL seguente mostra un esempio di aggiunta di una tabella a un database o a uno schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Impossibile aggiungere tabelle e viste ADLS a database/schemi DWH.


#### RIMUOVI SCHEMA

La query SQL seguente mostra un esempio di rimozione di una tabella da un database o da uno schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> Le tabelle e le viste DWH non possono essere rimosse da database/schemi DWH fisicamente collegati.


**Parametri**

| Elemento “parameters” | Descrizione |
| ------ | ------ |
| `table_name` | Nome della tabella che si sta modificando. |
| `column_name` | Nome della colonna che si desidera aggiungere. |
| `data_type` | Tipo di dati della colonna che si desidera aggiungere. I tipi di dati supportati sono: bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### MOSTRA CHIAVI PRIMARIE

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


### MOSTRA GRUPPI DI DATI

Il comando `SHOW DATAGROUPS` restituisce una tabella di tutti i database associati. Per ogni database, la tabella include schema, tipo di gruppo, tipo figlio, nome figlio e ID figlio.

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


### MOSTRA DATAGROUPS PER tabella

Il comando `SHOW DATAGROUPS FOR 'table_name'` restituisce una tabella di tutti i database associati che contengono il parametro come relativo elemento figlio. Per ogni database, la tabella include schema, tipo di gruppo, tipo figlio, nome figlio e ID figlio.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parametri**

- `table_name`: nome della tabella per la quale si desidera trovare i database associati.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
