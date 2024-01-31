---
title: Approfondimenti destinazioni
description: Scopri le istruzioni SQL che alimentano gli insight sulle destinazioni e utilizza queste query per generare insights personalizzati per esplorare ulteriormente l’attivazione dei dati da Adobe Experience Platform.
source-git-commit: 3d5dd6300952409e2dddb32eb11547fb43a5feac
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# Informazioni sulle destinazioni

Le informazioni derivate dall’analisi del modello dati rendono i dati di Adobe Real-time Customer Data Platform più accessibili, comprensibili e di impatto per il processo decisionale.

Comprendi le informazioni sulla destinazione accedendo all’SQL che le alimenta, quindi genera informazioni personalizzate per esplorare ulteriormente l’attivazione dei dati da Adobe Experience Platform alle piattaforme di destinazione. Trasforma i dati non elaborati in nuove informazioni fruibili utilizzando l’SQL esistente del modello dati di Real-Time CDP come ispirazione per creare query per le tue esigenze aziendali specifiche.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI.  -->

Le informazioni seguenti sono tutte disponibili per l&#39;utilizzo come parte del [Dashboard delle destinazioni](../guides/destinations.md) o un personalizzato [dashboard definito dall&#39;utente](../user-defined-dashboards.md). Consulta la [panoramica sulla personalizzazione](../customize/overview.md) per istruzioni su come personalizzare il dashboard o [creare e modificare nuovi widget](../customize/custom-widgets.md) nella libreria widget e [dashboard definito dall&#39;utente](../user-defined-dashboards.md#create-widget).

## Pubblico attivato {#activated-audiences}

Domande a cui questa informazione ha risposto:

- Qual è il conteggio totale dei tipi di pubblico attivati filtrati da una particolare destinazione?
- Qual è il numero di tipi di pubblico attivati da ciascuna destinazione?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Consulta la [Documentazione dei widget di tipi di pubblico attivati](../guides/destinations.md#activated-audiences) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Tipi di pubblico attivati su tutte le destinazioni {#activated-audiences-across-all-destinations}

Domande a cui questa informazione ha risposto:

- Quanti tipi di pubblico vengono attivati su tutte le destinazioni?
- Qual è il conteggio totale dei tipi di pubblico attivati?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Consulta la [Documentazione dei tipi di pubblico attivati su tutte le destinazioni dei widget](../guides/destinations.md#activated-audiences-across-all-destinations) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Destinazioni attive per piattaforma di destinazione {#active-destinations-by-destination-platform}

Domande a cui questa informazione ha risposto:

- Quante destinazioni sono attive?
- Qual è la suddivisione delle destinazioni attive per piattaforma di destinazione?
- Qual è il numero di destinazioni attive suddiviso per ogni piattaforma di destinazione?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Consulta la [Documentazione delle destinazioni attive per widget piattaforma di destinazione](../guides/destinations.md#active-destinations-by-destination-platform) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Tendenza delle dimensioni del pubblico {#audience-size-trend}

Domande a cui questa informazione ha risposto:

- In che modo la dimensione del pubblico è cambiata nel tempo, incluse le anomalie per un pubblico mappato su una destinazione?
- Come trovo la tendenza complessiva in termini di dimensioni del pubblico, per destinazione, nei periodi specificati di 30 giorni, 90 giorni e 12 mesi?
- Quali sono le caratteristiche chiave del pubblico che contribuisce alla dimensione, ad esempio i picchi relativi alle campagne di e-mail marketing?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Consulta la [Documentazione del widget tendenza dimensione pubblico](../guides/destinations.md#audience-size-trend) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Segmenti di pubblico comuni {#common-audiences}

Domande a cui questa informazione ha risposto:

- Quali sono i tipi di pubblico comuni tra due destinazioni diverse?
- Quanti profili ha ciascuno dei tipi di pubblico comuni tra due destinazioni diverse?
- Qual è il pubblico più grande a cui sono mappate due destinazioni?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Consulta la [Documentazione del widget Tipi di pubblico comuni](../guides/destinations.md#common-audiences) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Stato della destinazione {#destination-status}

Domande a cui questa informazione ha risposto:

- Qual è il numero totale di destinazioni abilitate per l’uso?
- Qual è il numero totale di destinazioni disabilitate?
- Qual è la suddivisione percentuale tra destinazioni abilitate e disabilitate?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulta la [Documentazione del widget di stato della destinazione](../guides/destinations.md#destination-status) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Conteggio delle destinazioni {#destinations-count}

Domande a cui questa informazione ha risposto:

- Quante destinazioni sono attualmente configurate?
- Come è cambiato nel tempo il numero totale di destinazioni?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Consulta la [Documentazione del widget di conteggio delle destinazioni](../guides/destinations.md#destinations-count) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Integrità del pubblico mappato {#mapped-audience-health}

Domande a cui questa informazione ha risposto:

- Quali tipi di pubblico mappati su una destinazione presentano variazioni significative negli ultimi 30 giorni?
- Qual è la dimensione più recente di un pubblico mappato e se è cambiato nell’ultimo mese?
- Come posso elencare tutti i tipi di pubblico mappati su una destinazione in base alla gravità delle modifiche di dimensione nell’ultimo mese?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Consulta la [Documentazione del widget di integrità del pubblico mappato](../guides/destinations.md#mapped-audience-health) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Pubblico mappato {#mapped-audiences}

Domande a cui questa informazione ha risposto:

- Quanti tipi di pubblico sono mappati a una particolare destinazione?
- Come è cambiato nel tempo il conteggio dei tipi di pubblico mappati?
- Dove posso confrontare due destinazioni per vedere la sovrapposizione di pubblico mappata su ciascuna destinazione?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Consulta la [Documentazione dei widget Pubblico mappato](../guides/destinations.md#mapped-audiences) per informazioni sull’aspetto e le funzionalità di questa informazione.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Destinazioni più utilizzate {#most-used-destinations}

Domande a cui questa informazione ha risposto:

- Quali sono le destinazioni più utilizzate?
- Quanti tipi di pubblico sono mappati su ogni destinazione, ordinati dal più alto al meno?
- In che modo la mappatura dei tipi di pubblico sulle destinazioni cambia da uno snapshot all’altro?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Consulta la [Documentazione dei widget delle destinazioni più utilizzate](../guides/destinations.md#most-used-destinations) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Tipi di pubblico attivati di recente {#recently-activated-audiences}

Domande a cui questa informazione ha risposto:

- A quale destinazione è stato attivato più di recente un pubblico?
- Come posso trovare un elenco di tutte le destinazioni in base alla data dell’ultimo aggiornamento?
- Come posso confrontare due destinazioni in base alle attivazioni più recenti?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Consulta la [Documentazione dei widget di tipi di pubblico attivati di recente](../guides/destinations.md#recently-activated-audiences) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Tipi di pubblico attivati di recente per destinazione {#recently-activated-audiences-by-destination}

Domande a cui questa informazione ha risposto:

- Quali tipi di pubblico vengono attivati per una particolare destinazione?
- Come trovo un elenco di tipi di pubblico attivati da un particolare pubblico dal più recente al meno recente?
- Come posso trovare un elenco di tipi di pubblico entro la data in cui è stato attivato per una destinazione specifica?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Consulta la [Documentazione dei tipi di pubblico attivati di recente per widget di destinazione](../guides/destinations.md#recently-activated-audiences-by-destination) per informazioni sull’aspetto e le funzionalità di questa informazione.

## Destinazioni create di recente {#recently-created-destinations}

Domande a cui questa informazione ha risposto:

- Quali sono le destinazioni create più di recente?
- Come trovo un elenco di destinazioni con la data di creazione?
- Quale nuova destinazione è stata creata di recente?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Consulta la [Documentazione del widget destinazioni create di recente](../guides/destinations.md#recently-created-destinations) per informazioni sull’aspetto e le funzionalità di questa informazione.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Passaggi successivi {#next-steps}

Una volta letto questo documento, potrai comprendere le istruzioni SQL che generano informazioni approfondite sul dashboard e quali sono le domande più comuni che vengono risolte dall’analisi. Ora puoi modificare e ripetere queste query SQL per generare informazioni personalizzate.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI. -->

Puoi anche leggere e comprendere il codice SQL che genera informazioni approfondite per [Profili](./profiles.md) e [Tipi di pubblico](./audiences.md) dashboard.

<!-- 
SQL MISSING FROM WIKI:
Unmapped audiences by identity
Mapped audiences by identity 
-->
