---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;scrittura query;scrittura query;home;popular topic;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: Linee guida generali per l’esecuzione di query in Query Service
type: Tutorial
description: Questo documento illustra dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 2%

---

# Linee guida generali per l&#39;esecuzione delle query in [!DNL Query Service]

Questo documento descrive dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform [!DNL Query Service].

Per informazioni dettagliate sulla sintassi SQL utilizzata in [!DNL Query Service], leggere la [documentazione relativa alla sintassi SQL](../sql/syntax.md).

## Modelli di esecuzione delle query

In Adobe Experience Platform [!DNL Query Service] sono disponibili due modelli di esecuzione delle query: interattivo e non interattivo. L’esecuzione interattiva viene utilizzata per lo sviluppo delle query e la generazione di rapporti negli strumenti di business intelligence, mentre la modalità non interattiva viene utilizzata per processi e query operative di grandi dimensioni come parte di un flusso di lavoro di elaborazione dei dati.

### Esecuzione di query interattive

Le query possono essere eseguite in modo interattivo inviandole tramite l&#39;interfaccia utente [!DNL Query Service] o [tramite un client connesso](../clients/overview.md). Quando si esegue [!DNL Query Service] tramite un client connesso, viene eseguita una sessione attiva tra il client e [!DNL Query Service] fino a quando non viene restituita la query inviata o si verifica un timeout.

L’esecuzione di query interattive presenta le seguenti limitazioni:

| Parametro | Limitazione |
| --------- | ---------- |
| Timeout query | 10 minuti |
| Numero massimo di righe restituite | 50.000 |
| Numero massimo di query concorrenti | 5 |

>[!NOTE]
>
>Per ignorare il limite massimo di righe, includere `LIMIT 0` nella query. Il timeout della query di 10 minuti è ancora valido.

Per impostazione predefinita, i risultati delle query interattive vengono restituiti al client e sono **non** persistenti. Per mantenere i risultati come set di dati in [!DNL Experience Platform], la query deve utilizzare la sintassi `CREATE TABLE AS SELECT`.

### Esecuzione di query non interattiva

Le query inviate tramite l&#39;API [!DNL Query Service] vengono eseguite in modo non interattivo. L&#39;esecuzione non interattiva indica che [!DNL Query Service] riceve la chiamata API ed esegue la query nell&#39;ordine in cui viene ricevuta. Le query non interattive generano sempre un nuovo set di dati in [!DNL Experience Platform] per la ricezione dei risultati o l&#39;inserimento di nuove righe in un set di dati esistente.

## Accesso a un campo specifico all’interno di un oggetto

Per accedere a un campo all&#39;interno di un oggetto nella query, è possibile utilizzare la notazione del punto (`.`) o la notazione della parentesi quadra (`[]`). L&#39;istruzione SQL seguente utilizza la notazione del punto per passare dall&#39;oggetto `endUserIds` all&#39;oggetto `mcid`.

>[!NOTE]
>
>L’ID Experience Cloud (ECID) è noto anche come MCID e continua a essere utilizzato nei namespace.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

L&#39;istruzione SQL seguente utilizza la notazione tra parentesi per scorrere l&#39;oggetto `endUserIds` fino all&#39;oggetto `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

>[!NOTE]
>
>Poiché ogni tipo di notazione restituisce gli stessi risultati, quello che si sceglie di utilizzare corrisponde alle proprie preferenze.

Entrambe le query di esempio di cui sopra restituiscono un oggetto appiattito, anziché un singolo valore:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

L&#39;oggetto `endUserIds._experience.mcid` restituito contiene i valori corrispondenti per i seguenti parametri:

- `id`
- `namespace`
- `primary`

Quando la colonna viene dichiarata solo per l&#39;oggetto, restituisce l&#39;intero oggetto come stringa. Per visualizzare solo l’ID, utilizza:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Virgolette

Le virgolette singole, le virgolette doppie e le virgolette posteriori hanno utilizzi diversi nelle query di Query Service.

### Virgolette singole

Virgolette singole (`'`) utilizzate per creare stringhe di testo. Può essere ad esempio utilizzato nell&#39;istruzione `SELECT` per restituire un valore di testo statico nel risultato e nella clausola `WHERE` per valutare il contenuto di una colonna.

La query seguente dichiara un valore di testo statico (`'datasetA'`) per una colonna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Nella query seguente viene utilizzata una stringa tra virgolette singole (`'homepage'`) nella clausola WHERE per restituire eventi per una pagina specifica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Virgolette doppie

Virgolette doppie (`"`) utilizzate per dichiarare un identificatore con spazi.

La query seguente utilizza le virgolette doppie per restituire i valori dalle colonne specificate quando una colonna contiene uno spazio nel relativo identificatore:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Le virgolette doppie **non possono** essere utilizzate con accesso al campo di notazione del punto.

### Virgolette posteriori

Le virgolette posteriori `` ` `` vengono utilizzate per l&#39;escape dei nomi di colonna riservati **only** quando si utilizza la sintassi di notazione del punto. Ad esempio, poiché `order` è una parola riservata in SQL, è necessario utilizzare le virgolette per accedere al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Le virgolette posteriori vengono inoltre utilizzate per accedere a un campo che inizia con un numero. Ad esempio, per accedere al campo `30_day_value`, è necessario utilizzare la notazione delle virgolette posteriori.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Le virgolette posteriori sono **non** necessarie se si utilizza la notazione tra parentesi quadre.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Visualizzazione delle informazioni della tabella

Dopo la connessione a Query Service, puoi visualizzare tutte le tabelle disponibili su Platform utilizzando i comandi `\d` o `SHOW TABLES`.

### Vista tabella standard

Il comando `\d` mostra la vista standard [!DNL PostgreSQL] per l&#39;elenco delle tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Vista tabella dettagliata

Il comando `SHOW TABLES` è un comando personalizzato che fornisce informazioni più dettagliate sulle tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informazioni schema

Per visualizzare informazioni più dettagliate sugli schemi all&#39;interno della tabella, è possibile utilizzare il comando `\d {TABLE_NAME}`, dove `{TABLE_NAME}` è il nome della tabella di cui si desidera visualizzare le informazioni sullo schema.

L&#39;esempio seguente mostra le informazioni sullo schema per la tabella `luma_midvalues`, che verrebbero visualizzate utilizzando `\d luma_midvalues`:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

È inoltre possibile ottenere ulteriori informazioni su una colonna specifica aggiungendo il nome della colonna al nome della tabella. Scritto nel formato `\d {TABLE_NAME}_{COLUMN}`.

L&#39;esempio seguente mostra informazioni aggiuntive per la colonna `web` e verrebbe richiamato utilizzando il comando seguente: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Unione di set di dati

Puoi unire più set di dati per includere nella query dati provenienti da altri set di dati.

L&#39;esempio seguente unisce i due set di dati seguenti (`your_analytics_table` e `custom_operating_system_lookup`) e crea un&#39;istruzione `SELECT` per i primi 50 sistemi operativi in base al numero di visualizzazioni di pagina.

**Query**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Risultati**

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| IOS per dispositivi mobili 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 e XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Deduplica

Query Service supporta la deduplicazione dei dati o la rimozione di righe duplicate dai dati. Per ulteriori informazioni sulla deduplicazione, leggere la [Guida alla deduplicazione di Query Service](../key-concepts/deduplication.md).

## Calcoli del fuso orario in Query Service

Query Service standardizza i dati persistenti in Adobe Experience Platform utilizzando il formato di marca temporale UTC. Per ulteriori informazioni su come tradurre il requisito del fuso orario da e verso un timestamp UTC, consulta la sezione [Domande frequenti su come modificare il fuso orario da e verso un timestamp UTC](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Passaggi successivi

La lettura di questo documento ha introdotto alcune importanti considerazioni durante la scrittura di query tramite [!DNL Query Service]. Per ulteriori informazioni su come utilizzare la sintassi SQL per scrivere query personalizzate, leggere la [documentazione sulla sintassi SQL](../sql/syntax.md).

Per ulteriori esempi di query che possono essere utilizzate in Query Service, consulta la seguente documentazione sul caso d’uso:

- [Informazioni su Analytics](../use-cases/analytics-insights.md)
- [Creare un rapporto con tendenze degli eventi](../use-cases/trended-report-of-events.md)
- [Visualizzare un rapporto aggregato di un visitatore](../use-cases/roll-up-report-of-a-visitor.md)
- [Elencare le visualizzazioni di pagina di un utente](../use-cases/list-visitor-sessions.md)
- [Elencare i visitatori in base al numero di visualizzazioni di pagina](../use-cases/visitors-by-number-of-page-views.md)
