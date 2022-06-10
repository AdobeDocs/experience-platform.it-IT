---
title: Analisi Delle Attività Con Adobe Target
description: Questo documento spiega come utilizzare Query Service per creare informazioni fruibili dai set di dati creati con i dati Adobe Target.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Analisi delle attività con Adobe Target

Adobe Experience Platform consente di acquisire dati da Adobe Target utilizzando i campi Experience Data Model (XDM) per creare set di dati da utilizzare con Query Service. Poiché Adobe Target è progettato per personalizzare il contenuto e personalizzare le esperienze utente, le query eseguite su questi set di dati consentono informazioni altamente personalizzate e mirate analizzando l’attività utente tramite SQL.

Questo documento fornisce una serie di query SQL di esempio che mostrano casi d&#39;uso comuni in base ai comportamenti e alle caratteristiche dei clienti.

## Introduzione

Per ciascuno dei seguenti casi d&#39;uso, viene fornito un esempio di query SQL con parametri come modello da personalizzare. Fornisci parametri ovunque vedi `{ }` negli esempi SQL che si desidera valutare.

## Mappatura del campo XDM parziale di alto livello

Nella tabella seguente sono elencati i campi di Target comuni e i campi XDM corrispondenti a cui sono mappati.

>[!NOTE]
>
>L&#39;uso di `[ ]` all’interno del campo XDM indica un array.

| Nome campo di destinazione | Nome campo XDM | Note |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | N/D |
| Attività ID | `_experience.target.activities.activityID` | N/D |
| ID esperienza | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | N/D |
| ID segmento | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | N/D |
| Ambito evento | `_experience.target.activities[].activityEvents[].eventScope` | Questo campo traccia i nuovi visitatori e visite. |
| ID passaggio | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Questo campo è un ID passaggio personalizzato per Adobe Campaign. |
| Totale prezzo | commerce.order.priceTotal | N/D |

>[!IMPORTANT]
>
>Il nome di un set di dati creato automaticamente utilizzando i dati di Target è &quot;Adobe Target Experience Events&quot;. Quando utilizzi questo set di dati con le query, utilizza il nome `adobe_target_experience_events`.

## Obiettivi

Analizzando le attività degli utenti, puoi personalizzare il contenuto per un pubblico specifico e testare versioni diverse del contenuto per una singola entità. Inoltre, analizzando un&#39;attività specifica in un determinato periodo di tempo o per i singoli utenti, le prestazioni di ogni singola attività possono essere meglio comprese. I risultati di questa analisi combinata possono essere utilizzati per comprendere le prestazioni di ogni singola attività.

I seguenti casi di utilizzo per la personalizzazione vengono creati utilizzando i dati di Adobe Target e si concentrano sulle attività degli utenti per creare informazioni utili sul comportamento dei clienti rispetto alle applicazioni aziendali.

Questa guida illustra i seguenti concetti chiave attraverso gli esempi di casi d’uso:

* Comprendere le prestazioni di un ID attività per un dato giorno, ad esempio conteggio, dettagli e ID esperienza associati.
* Per determinare l’ambito del visitatore e dell’evento per un’attività.
* Per raccogliere il conteggio dei visitatori, le visite e le informazioni sulle impression per Experience ID, Segment ID e Activity ID.

### Genera il conteggio delle attività orarie per un dato giorno

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

### Genera dettagli orari per un particolare specifico

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

### Determinare l’elenco degli ID esperienza per una specifica attività per un dato giorno

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

### Determinare il numero di visitatori, visite e impression per attività per un dato giorno

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

### Determinare visitatori, visite e impression per Experience ID, Segment ID e EventScope per un dato giorno

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
