---
title: Edizione B2C del modello dati di Real-time Customer Data Platform Insights
description: Scopri come utilizzare le query SQL con Real-time Customer Data Platform Insights Data Models (B2C Edition) per personalizzare i rapporti di Real-Time CDP per i casi d’uso di marketing e KPI.
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Edizione B2C del modello dati di Real-time Customer Data Platform Insights

Il modello dati di Real-time Customer Data Platform Insights per [B2C Edition](../../rtcdp/overview.md#rtcdp-b2c) espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per vari widget di profilo, destinazione e segmentazione. Puoi personalizzare questi modelli di query SQL per creare rapporti di Real-Time CDP per i casi d’uso degli indicatori di prestazioni chiave (KPI, Key Performance Indicator) e di marketing. Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard definite dall’utente. Consulta la documentazione sulle informazioni di reporting per l&#39;archivio accelerato delle query per scoprire [come creare un modello dati per le informazioni di reporting tramite Query Service da utilizzare con dati di archivio accelerato e dashboard definiti dall&#39;utente](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).

>[!NOTE]
>
>Il termine &quot;segmento&quot; è stato aggiornato a &quot;pubblico&quot; in tutti i sistemi Adobe Experience Platform. Alcuni riferimenti ai segmenti rimangono in uso per i percorsi dei file e le convenzioni di denominazione dei set di dati.

## Prerequisiti

Questa guida richiede una buona conoscenza della funzionalità [delle dashboard definite dall&#39;utente](../standard-dashboards.md). Leggi la documentazione prima di continuare con questa guida.

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

![ERD del modello di profilo.](../images/cdp-insights/profile-model.png)

#### Caso di utilizzo del conteggio dei profili {#profile-count}

La logica utilizzata per il widget [!UICONTROL Conteggio profili] restituisce il numero totale di profili uniti nell&#39;archivio profili al momento dello snapshot. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione del widget numero di profili]](../guides/profiles.md#profile-count).

L&#39;istruzione SQL che genera il widget [!UICONTROL Conteggio profili] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Caso di utilizzo: profili di identità singoli {#single-identity-profiles}

La logica utilizzata per il widget [!UICONTROL Profili di identità singoli] fornisce un conteggio dei profili dell&#39;organizzazione che hanno un solo tipo di ID che crea la loro identità. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione dei profili di identità singola]](../guides/profiles.md#single-identity-profiles).

L&#39;istruzione SQL che genera il widget [!UICONTROL Profili di identità singoli] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

### Modello dello spazio dei nomi {#namespace-model}

Il modello dello spazio dei nomi è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello dello spazio dei nomi.](../images/cdp-insights/namespace-model.png)

#### Profili per caso di utilizzo dell’identità {#profiles-by-identity}

Il widget [!UICONTROL Profili per identità] visualizza il raggruppamento di identità in tutti i profili uniti nell&#39;archivio profili. Per ulteriori informazioni, consulta la documentazione sui [[!UICONTROL profili per identità] widget](../guides/profiles.md#profiles-by-identity).

L&#39;istruzione SQL che genera il widget [!UICONTROL Profili per identità] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

#### Profili di identità singoli per caso di utilizzo dell’identità {#single-identity-profiles-by-identity}

La logica utilizzata per il widget [!UICONTROL Profili di identità singola per identità] illustra il numero totale di profili identificati con un solo identificatore univoco. Per ulteriori informazioni, consulta la [documentazione dei profili di identità singola per widget identità](../guides/profiles.md#single-identity-profiles-by-identity).

L&#39;istruzione SQL che genera i [!UICONTROL profili di identità singola per widget identità] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
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

![ERD del modello di pubblico.](../images/cdp-insights/audience-model.png)

#### Caso di utilizzo: dimensione del pubblico {#audience-size}

La logica utilizzata per il widget [!UICONTROL Dimensione pubblico] restituisce il numero totale di profili uniti all&#39;interno del pubblico selezionato al momento dello snapshot più recente. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione del widget Dimensione pubblico]](../guides/audiences.md#audience-size).

L&#39;istruzione SQL che genera il widget [!UICONTROL Dimensione pubblico] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

#### Caso di utilizzo: modifica della tendenza delle dimensioni del pubblico {#audience-size-change-trend}

La logica utilizzata per il widget [!UICONTROL Tendenza modifica dimensione pubblico] fornisce un grafico a linee che illustra la differenza nel numero totale di profili idonei per un determinato pubblico tra le istantanee giornaliere più recenti. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione del widget tendenza modifica dimensione pubblico]](../guides/audiences.md#audience-size-change-trend).

L&#39;istruzione SQL che genera il widget [!UICONTROL Tendenza modifica dimensione pubblico] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

#### Caso di utilizzo: destinazioni più utilizzate {#most-used-destinations}

La logica utilizzata nel widget [!UICONTROL Destinazioni più utilizzate] elenca le destinazioni più utilizzate della tua organizzazione in base al numero di tipi di pubblico mappati a esse. Questa classificazione fornisce informazioni approfondite sulle destinazioni utilizzate, mostrando potenzialmente anche quelle che potrebbero essere sottoutilizzate. Per ulteriori informazioni, consulta la documentazione sul widget [[!UICONTROL Destinazioni più utilizzate]](../guides/destinations.md#most-used-destinations).

L&#39;istruzione SQL che genera il widget [!UICONTROL Destinazioni più utilizzate] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

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

#### Caso di utilizzo di tipi di pubblico attivati di recente {#recently-activated-audiences}

La logica per il widget [!UICONTROL Tipi di pubblico attivati di recente] fornisce un elenco degli ultimi tipi di pubblico mappati su una destinazione. Questo elenco fornisce un’istantanea dei tipi di pubblico e delle destinazioni attivamente utilizzati nel sistema e può essere utile per risolvere eventuali mappature errate. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione sui widget dei tipi di pubblico attivati di recente]](../guides/destinations.md#recently-activated-audiences).

L&#39;istruzione SQL che genera il widget [!UICONTROL Tipi di pubblico attivati di recente] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

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

### Modello spazio dei nomi-pubblico {#namespace-audience-model}

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

![ERD del modello di pubblico-spazio dei nomi.](../images/cdp-insights/namespace-audience-model.png)

#### Profili per identità per un caso di utilizzo di pubblico {#audience-profiles-by-identity}

La logica utilizzata nel widget [!UICONTROL Profili per identità] fornisce un raggruppamento di identità in tutti i profili uniti nell&#39;archivio profili per un determinato pubblico. Per ulteriori informazioni, consulta la documentazione sui [[!UICONTROL profili per identità] widget](../guides/audiences.md#profiles-by-identity).

L&#39;istruzione SQL che genera il widget [!UICONTROL Profili per identità] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

### Modello di sovrapposizione dello spazio dei nomi

Il modello dello spazio dei nomi di sovrapposizione è costituito dai seguenti set di dati:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

L’immagine seguente contiene i campi di dati rilevanti in ogni set di dati.

![ERD del modello dello spazio dei nomi di sovrapposizione.](../images/cdp-insights/overlap-namespace-model.png)

#### Caso di utilizzo di sovrapposizione identità (profili) {#profiles-identity-overlap}

La logica utilizzata nel widget [!UICONTROL Sovrapposizione identità] visualizza la sovrapposizione dei profili nell&#39;**archivio profili** che contengono le due identità selezionate. Per ulteriori informazioni, consulta la sezione del widget [[!UICONTROL Sovrapposizione identità] nella documentazione del dashboard [!UICONTROL Profili]](../guides/profiles.md#identity-overlap).

L&#39;istruzione SQL che genera il widget di sovrapposizione [!UICONTROL identità] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

### Sovrapposizione dello spazio dei nomi per modello di pubblico {#overlap-namespace-by-audience-model}

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

![ERD dello spazio dei nomi di sovrapposizione per modello di pubblico.](../images/cdp-insights/overlap-namespace-by-audience-model.png)

#### Caso di utilizzo di sovrapposizione identità (tipi di pubblico) {#audiences-identity-overlap}

La logica utilizzata nel widget [!UICONTROL Tipi di pubblico] della dashboard [!UICONTROL Sovrapposizione identità] illustra la sovrapposizione dei profili che contengono le due identità selezionate per un determinato pubblico. Per ulteriori informazioni, consulta la sezione del widget [[!UICONTROL Sovrapposizione identità] nella documentazione del dashboard [!UICONTROL Tipi di pubblico]](../guides/audiences.md#identity-overlap).

L&#39;istruzione SQL che genera il widget di sovrapposizione [!UICONTROL identità] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### Overlap Namespace-Audience model {#overlap-namespace-audience-model}

The overlap namespace-audience model is comprised of the following datasets: 

- `adwh_fact_profile_overlap_by_namespace_and_segment`
- `adwh_dim_date`
- `adwh_dim_namespace`
- `adwh_dim_overlap_namespaces`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

![An ERD of the overlap namespace-audience model.](../images/cdp-insights/overlap-namespace-audience-model.png) -->

<!-- What insights are gathered from this particular data model? -->

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### AI model {#ai-model}

The AI model is comprised of the following datasets: 

- `adwh_fact_profile_ai_models`
- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_ai_models`

![An ERD of the AI model.](./images/cdp-insights/ai-model.png) -->

<!-- What insights are gathered from this particular data model? -->

