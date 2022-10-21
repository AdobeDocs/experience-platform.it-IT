---
title: Modello dati di Real-time Customer Data Platform Insights
description: Scopri come utilizzare le query SQL con i modelli di dati di Real-time Customer Data Platform Insights per personalizzare i tuoi report Real-Time CDP per i tuoi casi d’uso di marketing e KPI.
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: 16ae8a16d8c4f7ec68a054e8d15a518f453a05c7
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%

---

# Modello dati di Real-time Customer Data Platform Insights

La funzione Real-time Customer Data Platform Insights Data Model espone i modelli di dati e le istruzioni SQL che consentono di acquisire informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti Real-Time CDP per i tuoi casi d’uso di marketing e indicatori di prestazioni chiave (KPI, Key Performance Indicator). Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Per ulteriori informazioni, consulta la documentazione sulle informazioni di reporting per archivio accelerato query . [come creare un modello di dati insights per la generazione di rapporti tramite Query Service per l’utilizzo con dati di archivio accelerati e dashboard definiti dall’utente](../query-service/query-accelerated-store/reporting-insights-data-model.md).

## Prerequisiti

Questa guida richiede una buona comprensione del [funzione dashboard definita dall&#39;utente](./user-defined-dashboards.md). Prima di continuare con questa guida, leggi la documentazione .

## Rapporti approfonditi e casi d’uso di Real-Time CDP

Il reporting di Real-Time CDP fornisce informazioni approfondite sui dati del profilo e sulla sua relazione con segmenti e destinazioni. Sono stati sviluppati diversi modelli di schema a stella per rispondere a diversi casi d’uso comuni di marketing e ogni modello di dati può supportare diversi casi d’uso.

>[!IMPORTANT]
>
>I dati utilizzati per la generazione di rapporti di Real-Time CDP sono accurati per un criterio di unione scelto e per lo snapshot giornaliero più recente.

### Modello di profilo {#profile-model}

Il modello di profilo è composto da tre set di dati:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello di profilo.](./images/cdp-insights/profile-model.png)

#### Caso di utilizzo del conteggio dei profili

La logica utilizzata per il widget di conteggio dei profili restituisce il numero totale di profili uniti all’interno dell’archivio profili al momento dell’acquisizione dello snapshot. Consulta la sezione [[!UICONTROL Numero di profili] documentazione del widget](./guides/profiles.md#profile-count) per ulteriori informazioni.

SQL che genera il [!UICONTROL Numero di profili] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

#### Caso di utilizzo dei profili di identità singoli

La logica utilizzata per [!UICONTROL Profili di identità singoli] widget fornisce un conteggio dei profili della tua organizzazione con un solo tipo di ID che ne crea l&#39;identità. Consulta la sezione[[!UICONTROL Profili di identità singoli] documentazione del widget](./guides/profiles.md#single-identity-profiles) per ulteriori informazioni.

SQL che genera il [!UICONTROL Profili di identità singoli] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

Il modello dello spazio dei nomi è composto dai seguenti set di dati:

- `adwh_fact_profile_by_namespace`
- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello dello spazio dei nomi.](./images/cdp-insights/namespace-model.png)

#### Profili per caso d’uso dell’identità

La [!UICONTROL Profili per identità] Il widget visualizza la suddivisione delle identità in tutti i profili uniti nel tuo archivio profili. Consulta la sezione [[!UICONTROL Profili per identità] documentazione del widget](./guides/profiles.md#profiles-by-identity) per ulteriori informazioni.

SQL che genera il [!UICONTROL Profili per identità] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

#### Singoli profili di identità per caso di utilizzo dell’identità

La logica utilizzata per [!UICONTROL Singoli profili di identità per identità] widget illustra il numero totale di profili identificati con un solo identificatore univoco. Consulta la sezione [Documentazione relativa ai singoli profili di identità per widget di identità](./guides/profiles.md#single-identity-profiles-by-identity) per ulteriori informazioni.

SQL che genera il [!UICONTROL Singoli profili di identità per identità] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

### Modello di segmento {#segment-model}

Il modello di segmento è composto dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_fact_profile_by_segment`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello di segmento.](./images/cdp-insights/segment-model.png)

#### Caso di utilizzo: dimensione del pubblico

La logica utilizzata per [!UICONTROL Dimensione del pubblico] widget restituisce il numero totale di profili uniti all’interno del segmento selezionato al momento dell’istantanea più recente. Consulta la sezione [[!UICONTROL Dimensione del pubblico] documentazione del widget](./guides/segments.md#audience-size) per ulteriori informazioni.

SQL che genera il [!UICONTROL Dimensione del pubblico] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

#### Caso di utilizzo della tendenza della modifica della dimensione del pubblico

La logica utilizzata per [!UICONTROL Tendenza al cambiamento della dimensione del pubblico] widget fornisce un grafico a linee che illustra la differenza nel numero totale di profili qualificati per un dato segmento tra le istantanee giornaliere più recenti. Consulta la sezione [[!UICONTROL Tendenza al cambiamento della dimensione del pubblico] documentazione del widget](./guides/segments.md#audience-size-change-trend) per ulteriori informazioni.

SQL che genera il [!UICONTROL Tendenza al cambiamento della dimensione del pubblico] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

#### Caso d’uso delle destinazioni più utilizzate

La logica utilizzata nel [!UICONTROL Destinazioni più utilizzate] In widget sono elencate le destinazioni più utilizzate della tua organizzazione in base al numero di segmenti mappati su di esse. Questa classificazione fornisce informazioni sulle destinazioni che vengono utilizzate, mostrando al contempo quelle che potrebbero essere sottoutilizzate. Consulta la documentazione sul [[!UICONTROL Destinazioni più utilizzate] widget](./guides/destinations.md#most-used-destinations) per ulteriori informazioni.

SQL che genera il [!UICONTROL Destinazioni più utilizzate] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

#### Caso di utilizzo dei segmenti attivati di recente

La logica per [!UICONTROL Segmenti attivati di recente] widget fornisce un elenco dei segmenti mappati più di recente a una destinazione. Questo elenco fornisce un’istantanea dei segmenti e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate. Consulta la sezione [[!UICONTROL Segmenti attivati di recente] documentazione del widget](./guides/destinations.md#recently-activated-segments) per ulteriori informazioni.

SQL che genera il [!UICONTROL Segmenti attivati di recente] widget è visto nella sezione comprimibile di seguito.

query +++SQL

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### Modello del segmento dello spazio dei nomi

Il modello namespace-segmento è composto dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello di segmento.](./images/cdp-insights/namespace-segment-model.png)

#### Profili per identità per caso d’uso di un segmento

La logica utilizzata nel [!UICONTROL Profili per identità] widget fornisce un raggruppamento di identità in tutti i profili uniti nel tuo archivio profili per un dato segmento. Consulta la sezione [[!UICONTROL Profili per identità] documentazione del widget](./guides/segments.md#profiles-by-identity) per ulteriori informazioni.

SQL che genera il [!UICONTROL Profili per identità] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

### Modello di spazio dei nomi di sovrapposizione

Il modello dello spazio dei nomi di sovrapposizione è composto dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello di segmento.](./images/cdp-insights/overlap-namespace-model.png)

#### Caso d’uso di sovrapposizione identità (profili)

La logica utilizzata nel [!UICONTROL Sovrapposizione identità] Il widget visualizza la sovrapposizione dei profili nel tuo **Archivio profili** che contengono le due identità selezionate. Per ulteriori informazioni, consulta la sezione [[!UICONTROL Sovrapposizione identità] sezione widget del [!UICONTROL Profili] documentazione del dashboard](./guides/profiles.md#identity-overlap).

SQL che genera il [!UICONTROL Sovrapposizione identità] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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

### Spazio dei nomi di sovrapposizione per modello di segmento

Lo spazio dei nomi di sovrapposizione per modello di segmento è composto dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

L’immagine seguente contiene i campi dati pertinenti in ogni set di dati.

![Un ERD del modello di segmento.](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### Caso d’uso di sovrapposizione identità (segmenti)

La logica utilizzata nel [!UICONTROL Segmenti] dashboard [!UICONTROL Sovrapposizione identità] widget illustra la sovrapposizione di profili che contengono le due identità selezionate per un particolare segmento. Per ulteriori informazioni, consulta la sezione [[!UICONTROL Sovrapposizione identità] sezione widget del [!UICONTROL Segmentazione] documentazione del dashboard](./guides/segments.md#identity-overlap).

SQL che genera il [!UICONTROL Sovrapposizione identità] widget è visto nella sezione comprimibile di seguito.

query +++SQL

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
