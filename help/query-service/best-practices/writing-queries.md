---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;scrivere query;scrivere query;'
solution: Experience Platform
title: Scrittura di query
topic: queries
type: Tutorial
description: In questo documento sono riportati i dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 3%

---


# Guida generale per l&#39;esecuzione delle query in [!DNL Query Service]

In questo documento sono riportati i dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform [!DNL Query Service].

Per informazioni dettagliate sulla sintassi SQL utilizzata in [!DNL Query Service], consultare la [documentazione relativa alla sintassi SQL](../sql/syntax.md).

## Modelli di esecuzione delle query

Adobe Experience Platform [!DNL Query Service] dispone di due modelli di esecuzione delle query: interattivo e non interattivo. L&#39;esecuzione interattiva viene utilizzata per lo sviluppo di query e la generazione di report in strumenti di business intelligence, mentre quella non interattiva viene utilizzata per processi e query operative più grandi come parte di un flusso di lavoro di elaborazione dati.

### Esecuzione di query interattive

Le query possono essere eseguite in modo interattivo inviandole tramite l&#39;interfaccia [!DNL Query Service] o [tramite un client connesso](../clients/overview.md). Quando si esegue [!DNL Query Service] attraverso un client connesso, una sessione attiva viene eseguita tra il client e [!DNL Query Service] finché la query inviata non restituisce un risultato o si verifica un timeout.

L&#39;esecuzione della query interattiva presenta le seguenti limitazioni:

| Parametro | Limitazione |
| --------- | ---------- |
| Timeout query | 10 minuti |
| Numero massimo di righe restituite | 50.000 |
| Numero massimo di query simultanee | 5 |

>[!NOTE]
>
>Per ignorare il limite massimo di righe, includi `LIMIT 0` nella query. È ancora valido il timeout della query di 10 minuti.

Per impostazione predefinita, i risultati delle query interattive vengono restituiti al client e sono **non** persistenti. Per mantenere i risultati come dataset in [!DNL Experience Platform], la query deve utilizzare la sintassi `CREATE TABLE AS SELECT`.

### Esecuzione query non interattiva

Le query inviate tramite l&#39;API [!DNL Query Service] vengono eseguite in modo non interattivo. L&#39;esecuzione non interattiva indica che [!DNL Query Service] riceve la chiamata API ed esegue la query nell&#39;ordine in cui viene ricevuta. Le query non interattive generano sempre un nuovo dataset in [!DNL Experience Platform] per ricevere i risultati, oppure l&#39;inserimento di nuove righe in un dataset esistente.

## Accesso a un campo specifico all&#39;interno di un oggetto

Per accedere a un campo all&#39;interno di un oggetto nella query, è possibile utilizzare la notazione punto (`.`) o parentesi quadre (`[]`). La seguente istruzione SQL utilizza la notazione del punto per scorrere l&#39;oggetto `endUserIds` verso il basso fino all&#39;oggetto `mcid`.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

L&#39;istruzione SQL seguente utilizza la notazione tra parentesi quadre per scorrere l&#39;oggetto `endUserIds` verso il basso fino all&#39;oggetto `mcid`.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Nome della tabella di analisi. |

>[!NOTE]
>
>Poiché ogni tipo di notazione restituisce gli stessi risultati, quello che si sceglie di utilizzare dipende dalle preferenze.

Entrambe le query di esempio sopra restituiscono un oggetto appiattito, anziché un singolo valore:

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

Quando la colonna è dichiarata solo verso il basso, restituisce l&#39;intero oggetto come una stringa. Per visualizzare solo l’ID, utilizza:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Preventivi

Le virgolette singole, le virgolette doppie e le virgolette posteriori hanno utilizzi diversi all&#39;interno delle query del servizio query.

### Virgolette singole

Le virgolette singole (`'`) vengono utilizzate per creare stringhe di testo. Ad esempio, può essere utilizzato nell&#39;istruzione `SELECT` per restituire un valore di testo statico nel risultato, e nella clausola `WHERE` per valutare il contenuto di una colonna.

La seguente query dichiara un valore di testo statico (`'datasetA'`) per una colonna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

La seguente query utilizza una stringa tra virgolette singole (`'homepage'`) nella clausola WHERE per restituire gli eventi per una pagina specifica.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Doppie virgolette

Le virgolette doppie (`"`) vengono utilizzate per dichiarare un identificatore con spazi.

La seguente query utilizza virgolette doppie per restituire valori da colonne specificate quando una colonna contiene uno spazio nel relativo identificatore:

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
>Le virgolette doppie **non possono essere utilizzate con l&#39;accesso al campo di notazione del punto.**

### virgolette posteriori

Le virgolette posteriori `` ` `` vengono utilizzate per evitare i nomi di colonna riservati **solo** quando si utilizza la sintassi della notazione del punto. Ad esempio, poiché `order` è una parola riservata in SQL, è necessario utilizzare le virgolette per accedere al campo `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Le virgolette posteriori sono utilizzate anche per accedere a un campo che inizia con un numero. Ad esempio, per accedere al campo `30_day_value`, è necessario utilizzare la notazione delle virgolette.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Le virgolette posteriori sono **non** necessarie se si utilizza la notazione tra parentesi.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Visualizzazione delle informazioni della tabella

Dopo aver effettuato la connessione a Query Service, è possibile visualizzare tutte le tabelle disponibili sulla piattaforma utilizzando i comandi `\d` o `SHOW TABLES`.

### Visualizzazione tabella standard

Il comando `\d` mostra la visualizzazione PostgreSQL standard per elencare le tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Visualizzazione tabella dettagliata

`SHOW TABLES` è un comando personalizzato che fornisce informazioni più dettagliate sulle tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informazioni sullo schema

Per visualizzare informazioni più dettagliate sugli schemi all&#39;interno della tabella, è possibile utilizzare il comando `\d {TABLE_NAME}`, dove `{TABLE_NAME}` è il nome della tabella di cui si desidera visualizzare le informazioni sullo schema.

L&#39;esempio seguente mostra le informazioni sullo schema per la tabella `luma_midvalues`, che viene visualizzata utilizzando `\d luma_midvalues`:

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

È inoltre possibile ottenere ulteriori informazioni su una particolare colonna aggiungendo il nome della colonna al nome della tabella. Questo verrà scritto nel formato `\d {TABLE_NAME}_{COLUMN}`.

L&#39;esempio seguente mostra informazioni aggiuntive per la colonna `web` e viene richiamato utilizzando il comando seguente: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Unione di set di dati

È possibile unire più set di dati per includere nella query i dati provenienti da altri set di dati.

Nell&#39;esempio seguente vengono uniti i due set di dati seguenti (`your_analytics_table` e `custom_operating_system_lookup`) e viene creata un&#39;istruzione `SELECT` per i primi 50 sistemi operativi in base al numero di visualizzazioni di pagina.

**Query**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Risultati**

| Sistema operativo | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
|  Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
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

## Deduplication

Servizio query supporta la deduplicazione dei dati o la rimozione di righe duplicate dai dati. Per ulteriori informazioni sulla deduplicazione, consultare la [Guida alla deduplicazione del servizio query](./deduplication.md).

## Passaggi successivi

Leggendo questo documento, sono state introdotte alcune considerazioni importanti durante la scrittura di query con [!DNL Query Service]. Per ulteriori informazioni sull&#39;utilizzo della sintassi SQL per scrivere le proprie query, consultare la [documentazione relativa alla sintassi SQL](../sql/syntax.md).

Per ulteriori esempi di query utilizzabili in Query Service, leggere le guide sulle [ query di esempio Adobe Analytics](./adobe-analytics.md), [ query di esempio Adobe Target](./adobe-target.md) o sulle [query di esempio ExperienceEvent](./experience-event-queries.md).