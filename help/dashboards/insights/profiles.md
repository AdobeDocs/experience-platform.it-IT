---
title: Approfondimenti profilo
description: Scopri il linguaggio SQL che attiva le informazioni sul profilo e utilizza queste query per generare informazioni personalizzate che esplorano ulteriormente i clienti e le loro esperienze utente.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 3%

---

# Approfondimenti profilo

Le informazioni derivate dall’analisi del modello dati rendono i dati di Adobe Real-time Customer Data Platform più accessibili, comprensibili e di impatto per il processo decisionale.

Comprendi le informazioni sul tuo profilo accedendo all’SQL che li alimenta, quindi genera le tue informazioni per esplorare ulteriormente i tuoi clienti e le loro esperienze utente che compongono i tuoi profili. Trasforma i dati non elaborati in nuove informazioni fruibili utilizzando l’SQL esistente del modello dati di Real-Time CDP come ispirazione per creare query per le tue esigenze aziendali specifiche.

Per ulteriori informazioni su come adattare le istruzioni SQL degli approfondimenti direttamente tramite l&#39;interfaccia utente di Platform, consulta la [Visualizza documentazione SQL](../view-sql.md).

Tutte le informazioni seguenti sono disponibili per l&#39;utilizzo come parte del [dashboard dei profili](../guides/profiles.md) o di un [dashboard personalizzato definito dall&#39;utente](../standard-dashboards.md). Consulta la [panoramica sulla personalizzazione](../customize/overview.md) per istruzioni su come personalizzare il dashboard o [creare e modificare nuovi widget](../customize/custom-widgets.md) nella libreria di widget e [dashboard definito dall&#39;utente](../standard-dashboards.md#create-widget).

## Sovrapposizione del pubblico con criterio di unione {#audience-overlap-by-merge-policy}

Domande a cui questa informazione ha risposto:

- Quali profili sono comuni a entrambi i tipi di pubblico?
- In che modo la sovrapposizione influisce sui tassi di coinvolgimento o di conversione?
- Come possono essere personalizzate le strategie di marketing per il segmento sovrapposto?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sulla sovrapposizione del pubblico da parte dei widget dei criteri di unione](../guides/profiles.md#audience-overlap-by-merge-policy).

## Rapporto di sovrapposizione pubblico {#audience-overlap-report}

Domande a cui questa informazione ha risposto:

- Quali sono i 50 tipi di pubblico più sovrapposti?
- Quali sono i 50 tipi di pubblico con meno sovrapposizioni?
- Come cambia il pattern di sovrapposizione in base al criterio di unione?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget per report di sovrapposizione pubblico](../guides/profiles.md#audience-overlap-report).

## Tipi di pubblico (conteggio) {#audiences}

Domande a cui questa informazione ha risposto:

- Quale criterio di unione viene utilizzato principalmente per la segmentazione?
- Qual è la distribuzione dei tipi di pubblico nei criteri di unione?
- Esistono cambiamenti significativi nel numero di tipi di pubblico per specifici criteri di unione nel tempo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

Consulta la [documentazione del widget Tipi di pubblico](../guides/profiles.md#audiences) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Tipi di pubblico mappati allo stato di destinazione {#audiences-mapped-to-destination-status}

Domande a cui questa informazione ha risposto:

- Qual è la distribuzione complessiva dei tipi di pubblico tra destinazioni mappate e non mappate?
- Quali destinazioni specifiche hanno il maggior numero di tipi di pubblico mappati?
- Quale percentuale del pubblico totale non è ancora stata mappata?
- Di questi tipi di pubblico non mappati, esistono schemi o tendenze associate?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui tipi di pubblico mappati al widget di stato della destinazione](../guides/profiles.md#audiences-mapped-to-destination-status).

## Dimensione pubblico {#audiences-size}

Domande a cui questa informazione ha risposto:

- Quale segmento di pubblico ha le dimensioni più grandi?
- Quali sono i cinque tipi di pubblico più grandi?
- In che modo la distribuzione delle dimensioni del pubblico cambia nel tempo per il pubblico principale?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget dimensione pubblico](../guides/profiles.md#audiences-size).

## Distribuzione dei punteggi tramite IA analisi clienti {#customer-ai-distribution-of-scores}

Domande a cui questa informazione ha risposto:

- Qual è la distribuzione dei punteggi tra contenitori per ciascuno dei modelli di IA per l’analisi dei clienti?
- Qual è la distribuzione dei punteggi per punteggi alti, medi e bassi?
- Qual è la suddivisione della distribuzione del punteggio per criterio di unione?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT b.model_name,
     b.model_type,
     CASE
         WHEN score >= 0
              AND score < 25 THEN 'LOW'
         WHEN score >= 25
              AND score < 75 THEN 'MEDIUM'
         WHEN score >= 75
              AND score <= 100 THEN 'HIGH'
     END bucket_name,
     CASE
         WHEN score >= 0
              AND score < 5 THEN '02.50'
         WHEN score >= 5
              AND score < 10 THEN '07.50'
         WHEN score >= 10
              AND score < 15 THEN '12.50'
         WHEN score >= 15
              AND score < 20 THEN '17.50'
         WHEN score >= 20
              AND score < 25 THEN '22.50'
         WHEN score >= 25
              AND score < 30 THEN '27.50'
         WHEN score >= 30
              AND score < 35 THEN '32.50'
         WHEN score >= 35
              AND score < 40 THEN '37.50'
         WHEN score >= 40
              AND score < 45 THEN '42.50'
         WHEN score >= 45
              AND score < 50 THEN '47.50'
         WHEN score >= 50
              AND score < 55 THEN '52.50'
         WHEN score >= 55
              AND score < 60 THEN '57.50'
         WHEN score >= 60
              AND score < 65 THEN '62.50'
         WHEN score >= 65
              AND score < 70 THEN '67.50'
         WHEN score >= 70
              AND score < 75 THEN '72.50'
         WHEN score >= 75
              AND score < 80 THEN '77.50'
         WHEN score >= 80
              AND score < 85 THEN '82.50'
         WHEN score >= 85
              AND score < 90 THEN '87.50'
         WHEN score >= 90
              AND score < 95 THEN '92.50'
         WHEN score >= 95
              AND score <= 100 THEN '97.50'
     END score_bins,
     Sum(CASE
             WHEN score >= 0
                  AND score < 25 THEN count_of_profiles
             WHEN score >= 25
                  AND score < 75 THEN count_of_profiles
             WHEN score >= 75
                  AND score <= 100 THEN count_of_profiles
         END) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
          CASE
              WHEN score >= 0
                   AND score < 25 THEN 'LOW'
              WHEN score >= 25
                   AND score < 75 THEN 'MEDIUM'
              WHEN score >= 75
                   AND score <= 100 THEN 'HIGH'
          END,
          CASE
              WHEN score >= 0
                   AND score < 5 THEN '02.50'
              WHEN score >= 5
                   AND score < 10 THEN '07.50'
              WHEN score >= 10
                   AND score < 15 THEN '12.50'
              WHEN score >= 15
                   AND score < 20 THEN '17.50'
              WHEN score >= 20
                   AND score < 25 THEN '22.50'
              WHEN score >= 25
                   AND score < 30 THEN '27.50'
              WHEN score >= 30
                   AND score < 35 THEN '32.50'
              WHEN score >= 35
                   AND score < 40 THEN '37.50'
              WHEN score >= 40
                   AND score < 45 THEN '42.50'
              WHEN score >= 45
                   AND score < 50 THEN '47.50'
              WHEN score >= 50
                   AND score < 55 THEN '52.50'
              WHEN score >= 55
                   AND score < 60 THEN '57.50'
              WHEN score >= 60
                   AND score < 65 THEN '62.50'
              WHEN score >= 65
                   AND score < 70 THEN '67.50'
              WHEN score >= 70
                   AND score < 75 THEN '72.50'
              WHEN score >= 75
                   AND score < 80 THEN '77.50'
              WHEN score >= 80
                   AND score < 85 THEN '82.50'
              WHEN score >= 85
                   AND score < 90 THEN '87.50'
              WHEN score >= 90
                   AND score < 95 THEN '92.50'
              WHEN score >= 95
                   AND score <= 100 THEN '97.50'
          END;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sulla distribuzione dei punteggi da parte di IA per l&#39;analisi dei clienti](../guides/profiles.md#customer-ai-distribution-of-scores).

## Riepilogo del punteggio di IA per l’analisi dei clienti {#customer-ai-scoring-summary}

Domande a cui questa informazione ha risposto:

- Qual è il riepilogo del punteggio per ciascuno dei modelli di IA per l’analisi dei clienti?
- In che modo i punteggi di tendenza di Customer AI cambiano per tipi di pubblico diversi?
- Come cambia il riepilogo del punteggio rispetto ad altri KPI nella panoramica dei profili?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione del widget di riepilogo del punteggio di Customer AI](../guides/profiles.md#customer-ai-scoring-summary).

## Sovrapposizione di identità {#identity-overlap}

Domande a cui questa informazione ha risposto:

- Qual è l&#39;intersezione comune tra [!UICONTROL Tipo di identità A] e [!UICONTROL Tipo di identità B]?
- Come posso perfezionare i tipi di pubblico dei clienti in base alla sovrapposizione di tipi di identità specifici per migliorare le strategie di marketing mirate?
- Quali insight possono essere ottenuti valutando le prestazioni della campagna all’interno delle aree intersecanti?
- Utilizzando questa informazione sulle prestazioni della campagna, come possono essere ottimizzate le attività di marketing future?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget di sovrapposizione identità](../guides/profiles.md#identity-overlap).

## Conteggio dei profili {#profile-count}

Domande a cui questa informazione ha risposto:

- Qual è il conteggio complessivo dei profili in Adobe Real-time Customer Data Platform?
- Come vengono distribuiti i profili in base ai criteri di unione?
- Quale criterio di unione ha il conteggio di profili più alto?

L’SQl che genera queste informazioni è il seguente:

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

Informazioni complete sull&#39;aspetto e sulle funzionalità di questa informazione sono disponibili nella [Guida del widget Conteggio profili](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count).

Consulta la [documentazione del widget del conteggio dei profili](../guides/profiles.md#profile-count) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Modifica del conteggio dei profili {#profile-count-change}

Domande a cui questa informazione ha risposto:

- Qual è la tendenza nelle modifiche del conteggio complessivo dei profili?
- Cosa ha causato picchi o cadute significativi nel conteggio dei profili?
- Esistono criteri di unione specifici che determinano la modifica del conteggio dei profili?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

Consulta la [documentazione del widget di modifica del conteggio dei profili](../guides/profiles.md#profile-count-change) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Tendenza modifica conteggio profili {#profile-count-change-trend}

Domande a cui questa informazione ha risposto:

- Qual è la tendenza generale nella variazione del conteggio dei profili negli ultimi 12 mesi in base al criterio di unione?
- Esistono pattern o fluttuazioni specifici nella variazione del conteggio dei profili negli ultimi 30 giorni che richiedono attenzione?
- Come cambia il conteggio dei profili negli ultimi 90 giorni rispetto alla tendenza generale?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Consulta la [documentazione del widget della tendenza di modifica del conteggio dei profili](../guides/profiles.md#profile-count-change-trend) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Tendenza conteggio dei profili {#profile-count-trend}

Domande a cui questa informazione ha risposto:

- Qual è la tendenza complessiva nel conteggio dei profili in base al criterio di unione negli ultimi 30 giorni?
- In base a questa tendenza, come si confronta con le tendenze a lungo termine (ad esempio, 90 giorni e 12 mesi)?
- Quale criterio di unione contribuisce maggiormente all’aumento o alla diminuzione del conteggio dei profili nei periodi di tempo specificati (30 giorni, 90 giorni e 12 mesi)?
- Esistono picchi o ribassi specifici nel conteggio dei profili che sono correlati a determinati eventi o periodi nell’arco temporale di 30 giorni?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

Consulta la [documentazione del widget di tendenza del conteggio dei profili](../guides/profiles.md#profile-count-trend) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Profili per identità {#profiles-by-identity}

Domande a cui questa informazione ha risposto:

- Nel conteggio totale dei profili, quale tipo di identità rappresenta una proporzione maggiore?
- Esistono differenze significative tra i tipi di identità?
- Qual è la distribuzione complessiva dei tipi di identità?
- Esistono differenze o anomalie significative nel conteggio delle identità?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui profili per widget identità](../guides/profiles.md#profiles-by-identity).

## Tendenza di modifica del conteggio dei profili {#profiles-count-change-trend}

Domande a cui questa informazione ha risposto:

- Qual è la tendenza generale nella variazione del conteggio dei profili negli ultimi 12 mesi, in base al criterio di unione?
- Esistono pattern o fluttuazioni specifici nel cambiamento del conteggio dei profili negli ultimi 30 giorni che richiedono attenzione?
- Come si confronta la modifica nel conteggio dei profili negli ultimi 90 giorni con la tendenza generale?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione del widget della tendenza di modifica del conteggio dei profili](../guides/profiles.md#profiles-count-change-trend).

## Tendenza di modifica del conteggio dei profili per identità {#profiles-count-change-trend-by-identity}

Domande a cui questa informazione ha risposto:

- Qual è la tendenza generale nella variazione del conteggio dei profili tra le diverse identità negli ultimi 12 mesi?
- Esistono tendenze di identità specifiche che mostrano cambiamenti significativi negli ultimi 30 giorni?
- In che modo le modifiche nel conteggio dei profili differiscono quando si confrontano le tendenze di 30 giorni, 90 giorni e 12 mesi per una particolare identità?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sulla modifica del conteggio dei profili in base al widget identità](../guides/profiles.md#profiles-count-change-trend-by-identity).

## Profili a identità singola {#single-identity-profiles}

Domande a cui questa informazione ha risposto:

- I dati di identità del cliente sono rappresentati in modo coerente con le singole identità?
- Quale percentuale della mia base di utenti è costituita da profili con un solo tipo di identità?
- Dei profili con un solo tipo di identità, in che modo questo influisce sulla completezza del profilo?
- Esiste una correlazione tra il tipo di identità più comune e il conteggio dei profili di identità singoli?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget per profili di identità singoli](../guides/profiles.md#single-identity-profiles).

## Profili di identità singola per identità {#single-identity-profiles-by-identity}

Domande a cui questa informazione ha risposto:

- Quanti clienti univoci si sono registrati con un’unica identità (ad esempio e-mail o numero di telefono)?
- Qual è la distribuzione dei singoli profili di identità tra diversi tipi di identità, ad esempio e-mail o numeri di telefono?
- Esistono pattern o cambiamenti di identità emergenti all’interno dei singoli profili di identità?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui profili di identità singola per widget identità](../guides/profiles.md#single-identity-profiles-by-identity).

## Profili non segmentati {#unsegmented-profiles}

Domande a cui questa informazione ha risposto:

- Quanti profili non fanno parte di un pubblico?
- Quale percentuale del pubblico totale è rappresentata da profili non segmentati?
- Eventuali criteri di unione contribuiscono a un numero elevato di profili non segmentati?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget di profili non segmentati](../guides/profiles.md#unsegmented-profiles).

## Passaggi successivi

Una volta letto questo documento, potrai comprendere le istruzioni SQL che generano informazioni approfondite sul dashboard e quali sono le domande più comuni che vengono risolte dall’analisi. Ora puoi modificare e ripetere le istruzioni SQL per generare informazioni personalizzate.

Per ulteriori informazioni su come adattare l&#39;istruzione SQL delle informazioni direttamente tramite l&#39;interfaccia utente di Platform, vedere la [Visualizza documentazione SQL](../view-sql.md).

È inoltre possibile leggere e comprendere il linguaggio SQL che genera informazioni approfondite per le [dashboard Tipi di pubblico](./audiences.md), [Profili account](./account-profiles.md) e [Destinazioni](./destinations.md).
