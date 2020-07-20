---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Query di esempio
topic: queries
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---


# Query di esempio per i dati  Adobe Target

I dati provenienti da  Adobe Target vengono trasformati in schema XDM di Experience Event e trasferiti [!DNL Experience Platform] come set di dati. Esistono molti casi di utilizzo [!DNL Query Service] con questi dati e le seguenti query di esempio devono essere compatibili con i set di dati  Adobe Target.

>[!NOTE]
>Negli esempi seguenti, sarà necessario modificare l&#39;SQL per compilare i parametri previsti per le query in base al set di dati, alle variabili o all&#39;intervallo di tempo che si desidera valutare. Fornite i parametri ovunque vi troviate `{ }` nell&#39;SQL.

## Nome set di dati standard per l&#39;origine dati Target in [!DNL Platform]:

 eventi esperienza Adobe Target (nome descrittivo) <br>`adobe_target_experience_events` (nome da utilizzare nella query)

## Mappatura del campo XDM parziale di alto livello

L&#39;uso di `[ ]` denotes un array

| Nome | Campo XDM | Note |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| Attività ID | `_experience.target.activities.activityID` |  |
| ID esperienza | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| ID segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| Ambito evento | `_experience.target.activities[].activityEvents[].eventScope` | Tiene traccia di nuove visite e visite |
| ID passo | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | ID passaggio personalizzato per la campagna |
| Totale prezzo | `commerce.order.priceTotal` |  |

## Conteggio delle attività orarie per un dato giorno

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## Dettagli orari per una specifica attività per un dato giorno

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
  _ACP_YEAR = {target_year} AND 
  _ACP_MONTH = {target_month} AND 
  _ACP_DAY = {target_day} AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## ID esperienza per una specifica attività per un dato giorno

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## Restituisce un elenco degli ambiti dell’evento (visitatore, visita, impression) per istanze per ID attività per un dato giorno

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## Restituisce il numero di visitatori, visite, impression per attività per un dato giorno

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## Restituisci visitatori, visite, impression per Experience ID, Segment ID e EventScope per un dato giorno

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE 
        _ACP_YEAR = {target_year} AND
        _ACP_MONTH = {target_month} AND 
        _ACP_DAY = {target_day} AND 
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

## Restituisce i nomi delle mbox e il conteggio dei record per un dato giorno

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  _ACP_YEAR= {target_year} AND 
  _ACP_MONTH= {target_month} AND 
  _ACP_DAY= {target_day}
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
