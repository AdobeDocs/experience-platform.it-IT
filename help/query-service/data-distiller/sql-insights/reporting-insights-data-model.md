---
title: Guida di Informazioni su Query Accelerated Store Reporting
description: Scopri come creare un modello dati per le informazioni di reporting tramite Query Service da utilizzare con dati di archivio accelerati e dashboard definiti dall’utente.
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# Guida alle informazioni sul reporting rapido per store

L’archivio con query accelerate consente di ridurre il tempo e la potenza di elaborazione necessari per ottenere informazioni critiche dai dati. In genere, i dati vengono elaborati a intervalli regolari (ad esempio, su base oraria o giornaliera), dove vengono create e riportate le visualizzazioni aggregate. L’analisi di questi rapporti generati dai dati aggregati deriva da informazioni mirate a migliorare le prestazioni aziendali. L’archivio con query accelerata fornisce un servizio di cache, concorrenza, un’esperienza interattiva e un’API senza stato. Tuttavia, presuppone che i dati siano preelaborati e ottimizzati per l’esecuzione di query aggregate e non per l’esecuzione di query di dati non elaborati.

L’archivio con query accelerata ti consente di creare un modello dati personalizzato e/o estendere un modello dati Adobe Real-Time Customer Data Platform esistente. Puoi quindi interagire con o incorporare le tue informazioni di reporting in un framework di reporting/visualizzazione a tua scelta. Per informazioni su come [personalizzare i modelli di query SQL per creare rapporti Real-Time CDP per i casi d&#39;uso di indicatori di prestazioni chiave (KPI) e marketing, consulta la documentazione del modello dati di Real-Time Customer Data Platform Insights](../../../dashboards/data-models/cdp-insights-data-model-b2c.md).

Il modello dati di Real-Time CDP di Adobe Experience Platform fornisce informazioni su profili, tipi di pubblico e destinazioni e abilita le dashboard di Real-Time CDP insight. Questo documento ti guida attraverso il processo di creazione del modello dati Reporting Insights e anche come estendere i modelli dati di Real-Time CDP in base alle esigenze.

## Prerequisiti

Questa esercitazione utilizza dashboard definite dall&#39;utente per visualizzare i dati dal modello dati personalizzato nell&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni su questa funzione, consulta la [documentazione delle dashboard definite dall&#39;utente](../../../dashboards/standard-dashboards.md).

## Introduzione

Lo SKU di Data Distiller è necessario per creare un modello dati personalizzato per le informazioni di reporting ed estendere i modelli dati di Real-Time CDP che contengono dati Experience Platform arricchiti. Consulta la documentazione [package](../../packaging.md), [guardrail](../../guardrails.md#query-accelerated-store) e [licensing](../../data-distiller/license-usage.md) relativa allo SKU di Data Distiller. Se non disponi dello SKU di Data Distiller, contatta il rappresentante dell’assistenza clienti Adobe per ulteriori informazioni.

## Creare un modello dati per informazioni di reporting

Questa esercitazione utilizza un esempio di creazione di un modello dati di audience insight. Se utilizzi una o più piattaforme per gli inserzionisti per raggiungere il pubblico, puoi utilizzare l’API dell’inserzionista per ottenere un conteggio approssimativo delle corrispondenze per il pubblico.

All’inizio, disponi di un modello dati iniziale dalle tue sorgenti (potenzialmente dall’API della piattaforma dell’inserzionista). Per ottenere una visualizzazione aggregata dei dati non elaborati, crea un modello di reporting insights come descritto nell’immagine seguente. Questo consente a un set di dati di ottenere i limiti superiore e inferiore della corrispondenza del pubblico.

![Diagramma relazionale di entità (ERD) del modello utente di insight per il pubblico.](../../images/data-distiller/sql-insights/audience-insight-user-model.png)

In questo esempio, la tabella/set di dati `externalaudiencereach` è basato su un ID e tiene traccia dei limiti inferiore e superiore per il conteggio delle corrispondenze. La tabella/set di dati della dimensione `externalaudiencemapping` mappa l&#39;ID esterno a una destinazione e a un pubblico in Experience Platform.

## Creazione di un modello per la generazione di rapporti di approfondimenti con Data Distiller

Creare quindi un modello insight di reporting (`audienceinsight` in questo esempio) e utilizzare il comando SQL `ACCOUNT=acp_query_batch and TYPE=QSACCEL` per assicurarsi che venga creato nell&#39;archivio accelerato. Quindi utilizzare Query Service per creare uno schema `audienceinsight.audiencemodel` per il database `audienceinsight`.

>[!NOTE]
>
>Lo SKU di Data Distiller è richiesto per il comando `ACCOUNT=acp_query_batch`. Senza di esso, nel data lake viene creato un modello dati regolare.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Creare tabelle, relazioni e compilare dati

Dopo aver creato il modello di insight per la generazione di rapporti di `audienceinsight`, creare le tabelle `externalaudiencereach` e `externalaudiencemapping` e stabilire relazioni tra di esse. Utilizzare quindi il comando `ALTER TABLE` per aggiungere un vincolo di chiave esterna tra le tabelle e definire una relazione. Nell&#39;esempio SQL seguente viene illustrato come eseguire questa operazione.

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
SELECT cast(null as int) audience_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Dopo la corretta esecuzione di entrambi i comandi `ALTER TABLE`, viene creata la relazione tra le tabelle fact e dimension.

Dopo l&#39;esecuzione delle istruzioni, utilizzare il comando `SHOW datagroups;` per restituire un elenco dei set di dati disponibili nell&#39;archivio accelerato da `audienceinsight.audiencemodel`. I risultati della tabella devono essere simili all’esempio fornito di seguito.

>[!IMPORTANT]
>
>Dall&#39;endpoint API senza stato `POST /data/foundation/query/accelerated-queries` di Query Service è possibile accedere solo ai dati nell&#39;archivio accelerato.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Eseguire una query sul modello dati di reporting di insight

Utilizzare Query Service per eseguire query sulla tabella delle dimensioni `audiencemodel.externalaudiencereach`. Di seguito è riportato un esempio di query.

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

I risultati delle tabelle includono un conteggio e un ID.

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

## Estendi il modello dati con il modello dati di Real-Time CDP Insights

Puoi estendere il modello di pubblico con ulteriori dettagli per creare una tabella di dimensioni più ricca. Ad esempio, puoi mappare il nome del pubblico e il nome della destinazione all’identificatore del pubblico esterno. A questo scopo, utilizza Query Service per creare o aggiornare un nuovo set di dati e aggiungerlo al modello di pubblico che combina tipi di pubblico e destinazioni con un’identità esterna. Il diagramma seguente illustra il concetto di questa estensione del modello dati.

![Un diagramma ERD che collega il modello dati di Real-Time CDP insight e il modello di archivio rapido per query.](../../images/data-distiller/sql-insights/updatingAudienceInsightUserModel.png)

## Creare tabelle dimensione per estendere il modello di reporting insights

Utilizzare Query Service per aggiungere attributi descrittivi chiave dai set di dati della dimensione Real-Time CDP arricchiti al modello dati `audienceinsight` e stabilire una relazione tra la fact table e la nuova tabella della dimensione. L’istruzione SQL seguente illustra come integrare le tabelle dimensioni esistenti nel modello dati per insights di reporting.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         audience_name,
         destination_status,
         a.destination_id,
         a.audience_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_audiences AS b
                      ON ( ( a.audience_id ) = ( b.audience_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Utilizzare il comando `SHOW datagroups;` per confermare la creazione della tabella dimensione `external_seg_dest_map` aggiuntiva.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Eseguire una query sul modello dati Exaccelerated Store Reporting Insights

Ora che il modello dati `audienceinsight` è stato potenziato, è possibile eseguire una query. L’istruzione SQL seguente mostra l’elenco delle destinazioni e dei tipi di pubblico mappati.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.audience_name,
       b.destination_status,
       b.destination_id,
       b.audience_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

La query restituisce tutti i set di dati nell’archivio con accelerazione query:

```console
ext_custom_audience_id | destination_name |       audience_name        | destination_status | destination_id | audience_id 
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

L&#39;istruzione SQL seguente fornisce un raggruppamento del conteggio delle corrispondenze per pubblico in una destinazione e un raggruppamento di ogni destinazione di pubblico per pubblico.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.audience_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.audience_name
ORDER BY b.destination_name
LIMIT  5000
```

L’immagine seguente fornisce un esempio delle possibili visualizzazioni personalizzate basate sul modello dati per insights di reporting.

![Un conteggio delle corrispondenze per destinazione e widget di pubblico creato dal nuovo modello dati Reporting Insights.](../../images/data-distiller/sql-insights/user-defined-dashboard-widget.png)

Il modello dati personalizzato si trova nell’elenco dei modelli dati disponibili nell’area di lavoro del dashboard definita dall’utente. Consulta la [guida alla dashboard definita dall&#39;utente](../../../dashboards/standard-dashboards.md) per informazioni su come utilizzare il modello dati personalizzato.
