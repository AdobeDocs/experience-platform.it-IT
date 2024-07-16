---
title: Audiences Insights
description: Scopri il linguaggio SQL che attiva le informazioni sul pubblico e utilizza queste query per generare informazioni personalizzate per esplorare ulteriormente i dati sul pubblico da Adobe Experience Platform.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 3%

---

# Informazioni su Audiences

Le informazioni derivate dall’analisi del modello dati rendono i dati di Adobe Real-time Customer Data Platform più accessibili, comprensibili e di impatto per il processo decisionale.

Comprendi le informazioni sul pubblico accedendo all’SQL che li alimenta, quindi genera le tue informazioni per esplorare ulteriormente le identità e i profili che compongono i tipi di pubblico. Trasforma i dati non elaborati in nuove informazioni fruibili utilizzando l’SQL esistente del modello dati di Real-Time CDP come ispirazione per creare query per le tue esigenze aziendali specifiche.

Per ulteriori informazioni su come adattare l&#39;istruzione SQL delle informazioni direttamente tramite l&#39;interfaccia utente di Platform, vedere la [Visualizza documentazione SQL](../view-sql.md).

Tutte le informazioni seguenti sono disponibili per l&#39;utilizzo come parte del [dashboard Tipi di pubblico](../guides/audiences.md) o di un [dashboard definito dall&#39;utente](../user-defined-dashboards.md) personalizzato. Consulta la [panoramica sulla personalizzazione](../customize/overview.md) per istruzioni su come personalizzare il dashboard o [creare e modificare nuovi widget](../customize/custom-widgets.md) nella libreria di widget e [dashboard definito dall&#39;utente](../user-defined-dashboards.md#create-widget).

Tutte le informazioni seguenti sono disponibili per l&#39;utilizzo come parte del [dashboard Tipi di pubblico](../guides/audiences.md) o di un dashboard personalizzato.

## Rapporto di sovrapposizione pubblico {#audience-overlap-report}

Domande a cui questa informazione ha risposto:

- Quali sono i primi 50 tipi di pubblico sovrapposti di un particolare pubblico filtrato?
- Quali sono i 50 tipi di pubblico meno sovrapposti di un particolare pubblico filtrato?
- In che modo cambia il pattern di sovrapposizione per un pubblico filtrato diverso?

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget per report di sovrapposizione pubblico](../guides/audiences.md#audience-overlap-report).

## Sovrapposizione del pubblico {#audience-overlap}

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
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

Consulta la [documentazione sui widget di sovrapposizione pubblico](../guides/audiences.md#audience-overlap) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Tendenza dimensione del pubblico {#audience-size-change-trend}

Domande a cui questa informazione ha risposto:

- Ci sono picchi o cali significativi nelle dimensioni del pubblico negli ultimi 30 giorni, 90 giorni o 12 mesi?
- In che modo la dimensione del pubblico cambia durante giorni specifici?
- Sono state rilevate anomalie o pattern ricorrenti di picchi o ribassi negli ultimi 12 mesi?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione del widget di tendenza per la modifica delle dimensioni del pubblico](../guides/audiences.md#audience-size-change-trend).

## Tendenza dimensione pubblico per identità {#audience-size-trend-by-identity}

Domande a cui questa informazione ha risposto:

- Il mio pubblico è in continua crescita, si sta stabilizzando o sta vivendo fluttuazioni?
- Esiste un’identità specifica che ha picchi o cali nella crescita dell’audience nel tempo?
- Ci sono delle anomalie nella crescita della mia identità nel tempo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

Per informazioni sull&#39;aspetto e sulle funzionalità di questa informazione, consulta la [documentazione sulle tendenze delle dimensioni del pubblico in base al widget identità](../guides/audiences.md#audience-size-trend-by-identity).

## Tendenza delle dimensioni del pubblico {#audience-size-trend}

Domande a cui questa informazione ha risposto:

- In che modo la dimensione del pubblico è cambiata nel tempo, comprese eventuali anomalie?
- Come posso trovare la tendenza complessiva in termini di dimensioni del pubblico nei periodi: 30 giorni, 90 giorni e 12 mesi?
- Quali sono le caratteristiche chiave del pubblico che contribuiscono alla sua dimensione? Ad esempio, picchi dovuti a campagne di e-mail marketing.

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

Consulta la [documentazione del widget tendenza dimensioni pubblico](../guides/audiences.md#audience-size-trend) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Dimensione del pubblico {#audience-size}

Domande a cui questa informazione ha risposto:

- Qual è la dimensione attuale del pubblico totale?
- In che modo la dimensione del pubblico corrente si confronta con i periodi precedenti o con tipi di pubblico specifici?
- Qual è l’impatto delle recenti campagne di marketing sulla dimensione del pubblico?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Consulta la [documentazione sul widget dimensione pubblico](../guides/audiences.md#audience-size) per informazioni sull&#39;aspetto e le funzionalità di questa informazione.

## Distribuzione dei punteggi tramite IA analisi clienti {#customer-ai-distribution-of-scores}

Domande a cui questa informazione ha risposto:

- Qual è la distribuzione del punteggio per ogni bucket del modello di IA per l’analisi dei clienti, filtrata per un pubblico selezionato?
- Qual è la distribuzione di punteggio di alto, medio e basso per un particolare pubblico?
- Qual è la suddivisione della distribuzione del punteggio per vari tipi di pubblico di interesse?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
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
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sulla distribuzione dei punteggi da parte di IA per l&#39;analisi dei clienti](../guides/audiences.md#customer-ai-distribution-of-scores).

## Riepilogo del punteggio di IA per l’analisi dei clienti {#customer-ai-scoring-summary}

Domande a cui questa informazione ha risposto:

- Qual è il riepilogo del punteggio per ciascuno dei modelli di IA per l’analisi dei clienti per un determinato pubblico?
- In che modo i punteggi di tendenza di Customer AI cambiano per tipi di pubblico diversi?
- In che modo il riepilogo del punteggio è simile agli altri KPI nella panoramica del pubblico?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione del widget di riepilogo del punteggio di Customer AI](../guides/audiences.md#customer-ai-scoring-summary).

## Sovrapposizione di identità {#identity-overlap}

Domande a cui questa informazione ha risposto:

- Qual è l&#39;intersezione comune tra [!UICONTROL Tipo di identità A] e [!UICONTROL Tipo di identità B] per un pubblico filtrato?
- Come posso perfezionare i tipi di pubblico dei clienti in base alla sovrapposizione di tipi di identità specifici, per migliorare le strategie di marketing mirate?
- Quali insight possono essere ottenuti valutando le prestazioni della campagna all’interno delle aree intersecanti?
- In base a queste informazioni, come possono essere ottimizzate le future attività di marketing?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui widget di sovrapposizione identità](../guides/audiences.md#identity-overlap).

## Profili per identità {#profiles-by-identity}

Domande a cui questa informazione ha risposto:

- Quale tipo di identità presenta la proporzione più elevata nel conteggio totale dei profili per un pubblico selezionato?
- Esistono disparità significative tra i tipi di identità per un pubblico selezionato?
- Qual è la distribuzione complessiva dei tipi di identità per pubblico?
- Esistono disparità o anomalie significative nel conteggio delle identità per i vari tipi di pubblico?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sui profili per widget identità](../guides/audiences.md#profiles-by-identity).

## Attivazioni pianificate {#scheduled-activations}

Domande a cui questa informazione ha risposto:

- Quali sono le date di inizio e di fine delle attivazioni con le prestazioni migliori per un particolare pubblico su una piattaforma specifica?
- Quali piattaforme sono state utilizzate maggiormente per le attivazioni pianificate di un particolare pubblico?
- Esistono schemi di utilizzo della piattaforma che potrebbero guidare le decisioni sull’assegnazione delle priorità o la diversificazione delle strategie di attivazione per un pubblico specifico?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

Per informazioni sull&#39;aspetto e le funzionalità di questa informazione, consulta la [documentazione sulle attivazioni pianificate](../guides/audiences.md#scheduled-activations).

## Passaggi successivi

Una volta letto questo documento, potrai comprendere le istruzioni SQL che generano informazioni approfondite sul dashboard e quali sono le domande più comuni che vengono risolte dall’analisi. Ora puoi modificare e ripetere le istruzioni SQL per generare informazioni personalizzate.

Per ulteriori informazioni su come adattare l&#39;istruzione SQL delle informazioni direttamente tramite l&#39;interfaccia utente di Platform, vedere la [Visualizza documentazione SQL](../view-sql.md).

È inoltre possibile leggere e comprendere l&#39;istruzione SQL che genera informazioni approfondite per le dashboard [Profili](./profiles.md), [Profili account](./account-profiles.md) e [Destinazioni](./destinations.md).
