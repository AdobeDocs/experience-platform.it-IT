---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;scrittura query;scrittura query;
solution: Experience Platform
title: Guida generale per l’esecuzione delle query nel servizio query
topic-legacy: queries
type: Tutorial
description: Questo documento delinea dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform Query Service.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 13e2248845734d985331653a17599f48aec0ebde
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 3%

---

# Indicazioni generali per l’esecuzione delle query in [!DNL Query Service]

Questo documento descrive dettagli importanti da conoscere durante la scrittura di query in Adobe Experience Platform [!DNL Query Service].

Per informazioni dettagliate sulla sintassi SQL utilizzata in [!DNL Query Service], leggi la [Documentazione sulla sintassi SQL](../sql/syntax.md).

## Modelli di esecuzione delle query

Adobe Experience Platform [!DNL Query Service] dispone di due modelli di esecuzione delle query: interattivo e non interattivo. L’esecuzione interattiva viene utilizzata per lo sviluppo di query e la generazione di report in strumenti di business intelligence, mentre quella non interattiva viene utilizzata per processi e query operative più grandi come parte di un flusso di lavoro di elaborazione dati.

### Esecuzione di query interattive

Le query possono essere eseguite in modo interattivo inviandole tramite [!DNL Query Service] Interfaccia o [tramite un client connesso](../clients/overview.md). In esecuzione [!DNL Query Service] attraverso un client connesso, una sessione attiva viene eseguita tra il client e [!DNL Query Service] fino a quando la query inviata non restituisce o non scade.

L’esecuzione della query interattiva presenta le seguenti limitazioni:

| Parametro | Limitazione |
| --------- | ---------- |
| Timeout query | 10 minuti |
| Numero massimo di righe restituite | 50.000 |
| Numero massimo di query simultanee | 5 |

>[!NOTE]
>
>Per ignorare la limitazione massima delle righe, includi `LIMIT 0` nella query. Si applica ancora il timeout della query di 10 minuti.

Per impostazione predefinita, i risultati delle query interattive vengono restituiti al client e sono **not** persistente. Per mantenere i risultati come set di dati in [!DNL Experience Platform], la query deve utilizzare `CREATE TABLE AS SELECT` sintassi.

### Esecuzione di query non interattive

Query inviate tramite [!DNL Query Service] Le API vengono eseguite in modo non interattivo. Per esecuzione non interattiva si intende [!DNL Query Service] riceve la chiamata API ed esegue la query nell’ordine in cui viene ricevuta. Le query non interattive generano sempre un nuovo set di dati in [!DNL Experience Platform] per ricevere i risultati o l’inserimento di nuove righe in un set di dati esistente.

## Accesso a un campo specifico all’interno di un oggetto

Per accedere a un campo all’interno di un oggetto nella query, è possibile utilizzare la notazione del punto (`.`) o la notazione parentesi graffa (`[]`). L&#39;istruzione SQL seguente utilizza la notazione del punto per scorrere il `endUserIds` fino a `mcid` oggetto.

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

L&#39;istruzione SQL seguente utilizza la notazione tra parentesi graffe per scorrere il `endUserIds` fino a `mcid` oggetto.

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
>Poiché ogni tipo di notazione restituisce gli stessi risultati, quello che si sceglie di utilizzare dipende dalle proprie preferenze.

Entrambe le query di esempio sopra restituiscono un oggetto appiattito, anziché un singolo valore:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Il restituito `endUserIds._experience.mcid` l&#39;oggetto contiene i valori corrispondenti per i seguenti parametri:

- `id`
- `namespace`
- `primary`

Quando la colonna viene dichiarata solo verso il basso all’oggetto, restituisce l’intero oggetto come stringa. Per visualizzare solo l&#39;ID, utilizza:

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

## Preventivi

Le virgolette singole, le virgolette doppie e le virgolette posteriori hanno utilizzi diversi all’interno delle query Query Service.

### Virgolette singole

Il preventivo unico (`'`) viene utilizzata per creare stringhe di testo. Ad esempio, può essere utilizzato nella `SELECT` per restituire un valore di testo statico nel risultato e nel `WHERE` per valutare il contenuto di una colonna.

La seguente query dichiara un valore di testo statico (`'datasetA'`) per una colonna:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

La seguente query utilizza una stringa tra virgolette singole (`'homepage'`) nella relativa clausola WHERE per restituire gli eventi per una pagina specifica.

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

Virgolette doppie (`"`) viene utilizzato per dichiarare un identificatore con spazi.

La query seguente utilizza virgolette doppie per restituire i valori delle colonne specificate quando una colonna contiene uno spazio nel relativo identificatore:

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
>Virgolette doppie **impossibile** viene utilizzato con l’accesso al campo della notazione del punto.

### Virgolette posteriori

La citazione posteriore `` ` `` viene utilizzato per l&#39;escape dei nomi di colonne riservate **only** quando si utilizza la sintassi della notazione del punto. Ad esempio, dal `order` è una parola riservata in SQL, per accedere al campo è necessario utilizzare le virgolette posteriori `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Le virgolette posteriori vengono utilizzate anche per accedere a un campo che inizia con un numero. Ad esempio, per accedere al campo `30_day_value`, è necessario utilizzare la notazione delle virgolette.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Le virgolette posteriori sono **not** necessaria se si utilizza la notazione tra parentesi.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Visualizzazione delle informazioni sulle tabelle

Dopo la connessione a Query Service, puoi visualizzare tutte le tabelle disponibili su Platform utilizzando `\d` o `SHOW TABLES` comandi.

### Vista a tabella standard

La `\d` mostra la visualizzazione PostgreSQL standard per l&#39;elenco delle tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Vista tabella dettagliata

`SHOW TABLES` è un comando personalizzato che fornisce informazioni più dettagliate sulle tabelle. Di seguito è riportato un esempio dell&#39;output di questo comando:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informazioni sullo schema

Per visualizzare informazioni più dettagliate sugli schemi all’interno della tabella, puoi utilizzare la `\d {TABLE_NAME}` comando, dove `{TABLE_NAME}` è il nome della tabella di cui si desidera visualizzare le informazioni sullo schema.

L&#39;esempio seguente mostra le informazioni dello schema per `luma_midvalues` tabella, che verrebbe visualizzata utilizzando `\d luma_midvalues`:

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

È inoltre possibile ottenere ulteriori informazioni su una particolare colonna aggiungendo il nome della colonna al nome della tabella. Questo sarebbe scritto nel formato `\d {TABLE_NAME}_{COLUMN}`.

L’esempio seguente mostra informazioni aggiuntive per il `web` e viene richiamato utilizzando il seguente comando: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Unione di set di dati

Puoi unire più set di dati per includere nella query i dati provenienti da altri set di dati.

L&#39;esempio seguente potrebbe unire i due set di dati seguenti (`your_analytics_table` e `custom_operating_system_lookup`) e crea un `SELECT` per i primi 50 sistemi operativi in base al numero di visualizzazioni di pagina.

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

| Sistema operativo | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
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

## Deduplica

Query Service supporta la deduplicazione dei dati o la rimozione di righe duplicate dai dati. Per ulteriori informazioni sulla deduplicazione, consulta la sezione [Guida alla deduplicazione di Query Service](./deduplication.md).

## Calcolo del fuso orario nel servizio query

Query Service standardizza i dati persistenti in Adobe Experience Platform utilizzando il formato di marca temporale UTC. Per ulteriori informazioni su come tradurre il requisito del fuso orario in e da una marca temporale UTC, consulta la [Sezione Domande frequenti su come cambiare il fuso orario in e da una marca temporale UTC](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Passaggi successivi

La lettura di questo documento ti ha introdotto ad alcune importanti considerazioni quando scrivi query utilizzando [!DNL Query Service]. Per ulteriori informazioni su come utilizzare la sintassi SQL per scrivere le proprie query, leggere il [Documentazione sulla sintassi SQL](../sql/syntax.md).

Per ulteriori esempi di query utilizzabili in Query Service, consulta la seguente documentazione del caso d’uso:

- [Informazioni approfondite su Analytics](../use-cases/analytics-insights.md)
- [Analisi delle attività con Adobe Target](../use-cases/activity-analysis-with-adobe-target.md)
- [Query di esempio ExperienceEvent](../sample-queries/experience-event.md).
