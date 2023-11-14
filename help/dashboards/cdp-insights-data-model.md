---
title: Modello dati di Real-time Customer Data Platform Insights
description: Scopri come utilizzare le query SQL con i modelli dati di Real-time Customer Data Platform Insights per personalizzare i rapporti Real-Time CDP per i casi d’uso di marketing e KPI.
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: e55bbba92b0e3b9c86a9962ffa0131dfb7c15e77
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# Modello dati di Real-time Customer Data Platform Insights

La funzione Real-time Customer Data Platform Insights Data Model espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti di Real-Time CDP per i casi d’uso degli indicatori di prestazioni chiave (KPI, Key Performance Indicator) e di marketing. Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Per informazioni, consulta la documentazione sulle informazioni di reporting per archivio accelerato delle query. [come creare un modello dati per le informazioni di reporting tramite Query Service da utilizzare con dati di archivio accelerati e dashboard definiti dall’utente](../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md).

## Prerequisiti

Questa guida richiede una buona conoscenza del [funzione delle dashboard definite dall&#39;utente](./user-defined-dashboards.md). Leggi la documentazione prima di continuare con questa guida.

## Rapporti di approfondimento su Real-Time CDP e casi d’uso

Il reporting di Real-Time CDP fornisce informazioni approfondite sui dati del profilo e sulla sua relazione con il pubblico e le destinazioni. Sono stati sviluppati diversi modelli di schema a stella per rispondere a una serie di casi d’uso comuni di marketing e ogni modello di dati può supportare diversi casi d’uso.

>[!IMPORTANT]
>
>I dati utilizzati per i rapporti di Real-Time CDP sono accurati per un criterio di unione scelto e per lo snapshot giornaliero più recente.

### Modello di profilo {#profile-model}

Il modello di profilo è costituito da tre set di dati:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello di profilo.](./images/cdp-insights/profile-model.png)

#### Caso di utilizzo del conteggio dei profili

La logica utilizzata per il widget del conteggio dei profili restituisce il numero totale di profili uniti nell’archivio profili al momento dello snapshot. Consulta la [[!UICONTROL Conteggio profili] documentazione widget](./guides/profiles.md#profile-count) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Conteggio profili] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Caso di utilizzo: profili di identità singoli

Logica utilizzata per [!UICONTROL Profili di identità singole] Il widget fornisce un conteggio dei profili della tua organizzazione che hanno un solo tipo di ID che crea la loro identità. Consulta la[[!UICONTROL Profili di identità singole] documentazione widget](./guides/profiles.md#single-identity-profiles) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Profili di identità singole] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### Modello dello spazio dei nomi {#namespace-model}

Il modello dello spazio dei nomi è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello di spazio dei nomi.](./images/cdp-insights/namespace-model.png)

#### Profili per caso di utilizzo dell’identità

Il [!UICONTROL Profili per identità] Il widget mostra il raggruppamento delle identità in tutti i profili uniti nel tuo archivio profili. Consulta la [[!UICONTROL Profili per identità] documentazione widget](./guides/profiles.md#profiles-by-identity) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Profili per identità] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### Profili di identità singoli per caso di utilizzo dell’identità

Logica utilizzata per [!UICONTROL Profili di identità singola per identità] Il widget mostra il numero totale di profili identificati con un solo identificatore univoco. Consulta la [Documentazione dei profili di identità singola per widget identità](./guides/profiles.md#single-identity-profiles-by-identity) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Profili di identità singola per identità] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### Modello del pubblico {#audience-model}

Il modello del pubblico è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello di pubblico.](./images/cdp-insights/audience-model.png)

#### Caso di utilizzo: dimensione del pubblico

Logica utilizzata per [!UICONTROL Dimensione pubblico] widget restituisce il numero totale di profili uniti all’interno del pubblico selezionato al momento dello snapshot più recente. Consulta la [[!UICONTROL Dimensione pubblico] documentazione widget](./guides/audiences.md#audience-size) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Dimensione pubblico] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### Caso di utilizzo: modifica della tendenza delle dimensioni del pubblico

Logica utilizzata per [!UICONTROL Tendenza di modifica della dimensione del pubblico] Il widget fornisce un grafico a linee che illustra la differenza tra il numero totale di profili idonei per un determinato pubblico per le istantanee giornaliere più recenti. Consulta la [[!UICONTROL Tendenza di modifica della dimensione del pubblico] documentazione widget](./guides/audiences.md#audience-size-change-trend) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Tendenza di modifica della dimensione del pubblico] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### Caso di utilizzo: destinazioni più utilizzate

Logica utilizzata nel [!UICONTROL Destinazioni più utilizzate] il widget elenca le destinazioni più utilizzate della tua organizzazione in base al numero di tipi di pubblico mappati ad esse. Questa classificazione fornisce informazioni approfondite sulle destinazioni utilizzate, mostrando potenzialmente anche quelle che potrebbero essere sottoutilizzate. Consulta la documentazione su [[!UICONTROL Destinazioni più utilizzate] widget](./guides/destinations.md#most-used-destinations) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Destinazioni più utilizzate] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### Caso di utilizzo di tipi di pubblico attivati di recente

La logica per [!UICONTROL Pubblico attivato di recente] Il widget fornisce un elenco degli ultimi tipi di pubblico mappati su una destinazione. Questo elenco fornisce uno snapshot dei tipi di pubblico e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate. Consulta la [[!UICONTROL Pubblico attivato di recente] documentazione widget](./guides/destinations.md#recently-activated-audiences) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Pubblico attivato di recente] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### Modello spazio dei nomi-pubblico

Il modello namespace-audience è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello namespace-audience.](./images/cdp-insights/namespace-audience-model.png)

#### Profili per identità per un caso di utilizzo di pubblico

Logica utilizzata nel [!UICONTROL Profili per identità] Il widget fornisce un raggruppamento di identità in tutti i profili uniti nel tuo archivio profili per un determinato pubblico. Consulta la [[!UICONTROL Profili per identità] documentazione widget](./guides/audiences.md#profiles-by-identity) per ulteriori informazioni.

SQL che genera il codice [!UICONTROL Profili per identità] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### Modello di sovrapposizione dello spazio dei nomi

Il modello dello spazio dei nomi di sovrapposizione è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello dello spazio dei nomi di sovrapposizione.](./images/cdp-insights/overlap-namespace-model.png)

#### Caso di utilizzo di sovrapposizione identità (profili)

Logica utilizzata nel [!UICONTROL Sovrapposizione identità] Il widget mostra la sovrapposizione dei profili nel **Archivio profili** che contengono le due identità selezionate. Per ulteriori informazioni, vedere [[!UICONTROL Sovrapposizione identità] sezione widget della [!UICONTROL Profili] documentazione del dashboard](./guides/profiles.md#identity-overlap).

SQL che genera il codice [!UICONTROL Sovrapposizione identità] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### Sovrapposizione dello spazio dei nomi per modello di pubblico

Lo spazio dei nomi di sovrapposizione per modello di pubblico è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD dello spazio dei nomi di sovrapposizione per modello di pubblico.](./images/cdp-insights/overlap-namespace-by-audience-model.png)

#### Caso di utilizzo di sovrapposizione identità (tipi di pubblico)

Logica utilizzata nel [!UICONTROL Tipi di pubblico] dashboard [!UICONTROL Sovrapposizione identità] Il widget illustra la sovrapposizione di profili che contengono le due identità selezionate per un determinato pubblico. Per ulteriori informazioni, vedere [[!UICONTROL Sovrapposizione identità] sezione widget della [!UICONTROL Tipi di pubblico] documentazione del dashboard](./guides/audiences.md#identity-overlap).

SQL che genera il codice [!UICONTROL Sovrapposizione identità] Il widget è visibile nella sezione comprimibile sottostante.

Query +++SQL

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
