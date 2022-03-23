---
keywords: Experience Platform;home;argomenti popolari;servizio query;query di esempio;query di esempio;query di esempio;adobe target;
solution: Experience Platform
title: Query di esempio per i dati di Adobe Target
topic-legacy: queries
description: I dati di Adobe Target vengono trasformati in schema XDM di Experience Event e acquisiti in Experience Platform come set di dati per te. Questo documento contiene query di esempio per l’utilizzo di Query Service con i set di dati Adobe Target.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: 76847d8286776a554e55209fa1b334c98b02d76b
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Query di esempio per i dati di Adobe Target

I dati acquisiti da Adobe Target vengono trasformati in schema XDM di Experience Event e acquisiti in Adobe Experience Platform come set di dati. Adobe Experience Platform Query Service facilita molti casi d’uso per questi dati e le seguenti query di esempio devono funzionare con i set di dati Adobe Target.

Ad Experience Platform, il nome di un set di dati creato automaticamente è &quot;Adobe Target Experience Events&quot;. Quando utilizzi questo set di dati con le query, utilizza il nome `adobe_target_experience_events`.

## Mappatura del campo XDM parziale di alto livello

L’elenco seguente mostra i campi di Target che vengono mappati sui campi XDM corrispondenti.

>[!NOTE]
>
> L&#39;uso di `[ ]` all’interno del campo XDM indica un array.

- mboxName: `_experience.target.mboxname`
- Attività ID: `_experience.target.activities.activityID`
- ID esperienza: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- ID segmento: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Ambito evento: `_experience.target.activities[].activityEvents[].eventScope`
   - Questo campo traccia i nuovi visitatori e visite.
- ID passaggio: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Questo campo è un ID passaggio personalizzato per Adobe Campaign.
- Totale prezzo: `commerce.order.priceTotal`

## Query di esempio

Le query seguenti mostrano esempi di query comunemente utilizzate con Adobe Target.

Negli esempi seguenti, sarà necessario modificare l&#39;SQL per compilare i parametri previsti per le query in base al set di dati, alle variabili o al periodo di tempo di cui si è interessati a valutare. Fornisci parametri ovunque vedi `{ }` in SQL.

### L’attività oraria conta per un dato giorno

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
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Dettagli orari per una specifica attività per un dato giorno

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### ID esperienza per un’attività specifica per un dato giorno

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Restituisce un elenco degli ambiti evento (visitatore, visita, impression) per istanze per ID attività per un dato giorno

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Restituisce il conteggio di visitatori, visite, impression per attività per un dato giorno

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
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Visitatori di ritorno, visite, impression per Experience ID, Segment ID e EventScope per un dato giorno

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
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
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

### Restituisce i nomi delle mbox e il conteggio dei record per un dato giorno

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
