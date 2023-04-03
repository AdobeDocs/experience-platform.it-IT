---
title: Guida agli approfondimenti dei rapporti sugli archivi accelerati delle query
description: Scopri come creare un modello di dati insights per la generazione di rapporti tramite Query Service per l’utilizzo con dati store accelerati e dashboard definiti dall’utente.
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Guida alle informazioni di reporting per store con accelerazione query

L’archivio accelerato delle query ti consente di ridurre il tempo e la potenza di elaborazione necessari per ottenere informazioni critiche dai tuoi dati. In genere, i dati vengono elaborati a intervalli regolari (ad esempio, su base oraria o giornaliera) in cui vengono create e riportate le visualizzazioni aggregate. L&#39;analisi di questi rapporti generati da dati aggregati deriva da informazioni intese a migliorare le prestazioni aziendali. L’archivio con accelerazione query fornisce un servizio cache, una concorrenza, un’esperienza interattiva e un’API senza stato. Tuttavia, presuppone che i dati siano preelaborati e ottimizzati per l’esecuzione di query aggregate e non per l’esecuzione di query sui dati non elaborati.

L’archivio con accelerazione query ti consente di creare un modello dati personalizzato e/o di estendere un modello dati Adobe Real-time Customer Data Platform esistente. Puoi quindi interagire con o incorporare le tue informazioni sui rapporti in un framework di reporting/visualizzazione a tua scelta. Per informazioni su come consultare la documentazione sul modello dati di Real-time Customer Data Platform Insights [personalizzare i modelli di query SQL per creare rapporti Real-Time CDP per i casi di utilizzo di marketing e indicatori prestazioni chiave (KPI, Key Performance Indicator)](../../../dashboards/cdp-insights-data-model.md).

Il modello dati Real-Time CDP di Adobe Experience Platform fornisce informazioni su profili, segmenti e destinazioni e abilita le dashboard approfondimenti di Real-Time CDP. Questo documento ti guida attraverso il processo di creazione del modello dati di reportistica insights e anche su come estendere i modelli di dati Real-Time CDP in base alle esigenze.

## Prerequisiti

Questa esercitazione utilizza dashboard definite dall’utente per visualizzare i dati dal modello dati personalizzato all’interno dell’interfaccia utente di Platform. Vedi la [documentazione delle dashboard definite dall&#39;utente](../../../dashboards/user-defined-dashboards.md) per ulteriori informazioni su questa funzione.

## Introduzione

Lo SKU di Data Distiller è necessario per creare un modello dati personalizzato per le informazioni di reporting e per estendere i modelli di dati di Real-Time CDP che contengono dati Platform arricchiti. Vedi la [imballaggio](../../packages.md) e [guardrail](../../guardrails.md#query-accelerated-store) documentazione relativa allo SKU di Data Distiller. Se non disponi della SKU di Data Distiller, contatta il tuo rappresentante del servizio clienti Adobe per ulteriori informazioni.

<!-- Document is hidden temporarily
Please see the [packaging](../../packages.md), [guardrails](../../guardrails.md#query-accelerated-store), and [licensing](../../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

## Creare un modello di dati insights per la generazione di rapporti

Questa esercitazione utilizza un esempio per creare un modello dati di audience insight. Se utilizzi una o più piattaforme inserzionista per raggiungere il pubblico, puoi utilizzare l’API dell’inserzionista per ottenere un conteggio approssimativo delle corrispondenze del pubblico.

All’inizio disponi di un modello dati iniziale dalle sorgenti (potenzialmente dall’API della piattaforma per gli inserzionisti). Per visualizzare in modo aggregato i dati grezzi, crea un modello di insights per la generazione di rapporti come descritto nell’immagine seguente. Questo consente a un set di dati di ottenere i limiti superiore e inferiore del pubblico corrispondente.

![Un diagramma relazionale di entità (ERD) del modello utente di informazioni sul pubblico.](../../images/query-accelerated-store/audience-insight-user-model.png)

In questo esempio, la `externalaudiencereach` table/dataset si basa su un ID e tiene traccia dei limiti inferiore e superiore per il conteggio delle corrispondenze. La `externalaudiencemapping` tabella/set di dati di dimensioni mappa l’ID esterno a una destinazione e a un segmento in Platform.

## Creare un modello per la creazione di rapporti approfonditi con Data Distiller

Quindi, crea un modello di informazioni di reporting (`audienceinsight` in questo esempio) e utilizzare il comando SQL `ACCOUNT=acp_query_batch and TYPE=QSACCEL` per garantire che venga creato sullo store accelerato. Quindi utilizza Query Service per creare un `audienceinsight.audiencemodel` schema per `audienceinsight` database.

>[!NOTE]
>
>La SKU di Data Distiller è necessaria per la `ACCOUNT=acp_query_batch` comando. Senza di essa, sul lago dati viene creato un modello dati regolare.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Creazione di tabelle, relazioni e compilazione di dati

Ora che hai creato il tuo `audienceinsight` modello di informazioni sul reporting, crea `externalaudiencereach` e `externalaudiencemapping` tabelle e stabilire relazioni tra loro. Quindi, utilizza `ALTER TABLE` per aggiungere un vincolo di chiave esterna tra le tabelle e definire una relazione. L&#39;esempio SQL seguente illustra come eseguire questa operazione.

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Dopo l&#39;esecuzione riuscita di entrambi `ALTER TABLE` viene formata la relazione tra le tabelle dei fatti e delle dimensioni.

Una volta eseguite le istruzioni, utilizza `SHOW datagroups;` per restituire un elenco dei set di dati disponibili nell&#39;archivio accelerato dal `audienceinsight.audiencemodel`. I risultati tabulati devono essere simili a quelli forniti di seguito.

>[!IMPORTANT]
>
>Solo i dati nell’archivio accelerato sono accessibili dall’endpoint API senza stato del servizio query `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Eseguire una query sul modello dati insight di reporting

Utilizzare Query Service per eseguire una query sul `audiencemodel.externalaudiencereach` tabella delle dimensioni. Di seguito è riportato un esempio di query.

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

I risultati tabulati includono un conteggio e un ID.

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## Estendi il tuo modello dati con il modello dati Real-Time CDP insights

Puoi estendere il modello di pubblico con ulteriori dettagli per creare una tabella di dimensioni più ricca. Ad esempio, puoi mappare il nome del segmento e il nome della destinazione all’identificatore esterno del pubblico. A questo scopo, utilizza Query Service per creare o aggiornare un nuovo set di dati e aggiungerlo al modello di pubblico che combina segmenti e destinazioni con un’identità esterna. Il diagramma seguente illustra il concetto di questa estensione del modello dati.

![Un diagramma ERD che collega il modello dati insight di Real-Time CDP e il modello di archivio con accelerazione query.](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Creare tabelle di dimensioni per estendere il modello di informazioni sui rapporti

Utilizza Query Service per aggiungere attributi descrittivi chiave dai set di dati delle dimensioni Real-Time CDP arricchiti al `audienceinsight` modello dati e stabilire una relazione tra la tabella dei fatti e la nuova tabella delle dimensioni. L&#39;istruzione SQL seguente illustra come integrare tabelle di dimensioni esistenti nel modello dati di analisi dei rapporti.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Utilizza la `SHOW datagroups;` per confermare la creazione dell&#39;ulteriore `external_seg_dest_map` tabella delle dimensioni.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Eseguire query sul modello dati approfonditi per la generazione di rapporti accelerati più ampi

Ora che `audienceinsight` il modello dati è stato potenziato ed è pronto per essere interrogato. Il seguente SQL mostra l&#39;elenco delle destinazioni e dei segmenti mappati.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

La query restituisce tutti i set di dati nell&#39;archivio con accelerazione query:

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## Visualizzare i dati con dashboard definiti dall’utente

Dopo aver creato il modello dati personalizzato, puoi visualizzare i dati con query personalizzate e dashboard definiti dall’utente.

Il seguente SQL fornisce un raggruppamento del numero di corrispondenze per audience in una destinazione e un raggruppamento di ciascuna destinazione di tipi di pubblico per segmento.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

L’immagine seguente fornisce un esempio delle possibili visualizzazioni personalizzate utilizzando il modello dati di reportistica di insights .

![Un conteggio delle corrispondenze per destinazione e widget di segmento creati dal nuovo modello dati di insights per la generazione di rapporti.](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

Il modello dati personalizzato si trova nell’elenco dei modelli dati disponibili nell’area di lavoro dashboard definita dall’utente. Consulta la sezione [guida utente al dashboard](../../../dashboards/user-defined-dashboards.md) per informazioni su come utilizzare il modello dati personalizzato.
