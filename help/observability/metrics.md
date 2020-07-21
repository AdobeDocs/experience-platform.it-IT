---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metriche disponibili
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# Elenco delle metriche disponibili

Le tabelle seguenti elencano tutte le metriche esposte da Approfondimenti di osservazione, suddivise per [!DNL Platform] servizio. Ogni metrica include una descrizione e il parametro di query ID accettato.

## [!DNL Data Ingestion]

La tabella seguente delinea le metriche per  Adobe Experience Platform [!DNL Data Ingestion]. Le metriche in **grassetto** sono metriche di assimilazione in streaming.

| Metrica Insights  | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Numero totale di set di dati creati. | N/D |
| timeseries.ingestion.dataset.size | Dimensione cumulativa di tutti i dati acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.dailysize | Dimensione dei dati acquisiti su base giornaliera per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.batchfailed.count | Numero di batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.batchsuccess.count | Numero di batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.recordsuccess.count | Numero di record acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.total.messages.rate** | Numero totale di messaggi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.valid.messages.rate** | Numero totale di messaggi validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.Invalid.messages.rate** | Numero totale di messaggi non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.type.count** | Numero totale di messaggi &quot;tipo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.range.count** | Numero totale di messaggi &quot;intervallo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.format.count** | Numero totale di messaggi &quot;formato&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.pattern.count** | Numero totale di messaggi &quot;pattern&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.presence.count** | Numero totale di messaggi di &quot;presenza&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.enum.count** | Numero totale di messaggi &quot;enum&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.unlassificati.count** | Numero totale di messaggi &quot;non classificati&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.validation.category.unknown.count** | Numero totale di messaggi &quot;sconosciuti&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| **timeseries.data.collection.inlet.total.messages.Received** | Numero totale di messaggi ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso (facoltativo) |
| **timeseries.data.collection.inlet.total.messages.size.Received** | Dimensione totale dei dati ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso (facoltativo) |
| **timeseries.data.collection.inlet.success** | Numero totale di chiamate HTTP riuscite a un&#39;entrata dati o a tutte le insenature dati. | ID ingresso (facoltativo) |
| **timeseries.data.collection.inlet.failure** | Numero totale di chiamate HTTP non riuscite a una entrata dati o a tutte le insenature dati. | ID ingresso (facoltativo) |

## [!DNL Identity Service]

La tabella seguente delinea le metriche per  Adobe Experience Platform [!DNL Identity Service].

| Metrica Insights  | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | Numero di record scritti nella propria origine dati da [!DNL Identity Service], per un set di dati o tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.identity.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Identity Service], per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | Numero di record di identità acquisiti correttamente per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | Numero di record di identità non riuscito da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | Numero di record di identità ignorati da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | Numero di identità univoche del grafico memorizzate nel grafico di identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS per una particolare intensità del grafico (&quot;sconosciuto&quot;, &quot;debole&quot; o &quot;forte&quot;). | Forza del grafico (**richiesta**) |

## [!DNL Privacy Service]

La tabella seguente delinea le metriche per  Adobe Experience Platform [!DNL Privacy Service].

| Metrica Insights  | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | Numero totale di posti di lavoro creati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.completedjobs.count | Numero totale di processi completati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.errorjobs.count | Numero totale di processi di errore da GDPR. | ENV (**obbligatorio**) |

## [!DNL Query Service]

La tabella seguente delinea le metriche per  Adobe Experience Platform [!DNL Query Service].

| Metrica Insights  | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | Numero totale di query pianificate non ricorrenti. | N/D |
| timeseries.queryservice.query.scheduledrecurring.count | Numero totale di query programmate ricorrenti. | N/D |
| timeseries.queryservice.query.batchquery.count | Numero totale di query batch eseguite. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Numero totale di query pianificate eseguite. | N/D |
| timeseries.queryservice.query.interactivequery.count | Numero totale di query interattive eseguite. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Numero totale di query batch eseguite da PSQL. | N/D |

## [!DNL Real-time Customer Profile]

La tabella seguente delinea le metriche per [!DNL Real-time Customer Profile].

| Metrica Insights  | Descrizione | Parametro query ID |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | Numero di record letti dal [!DNL Data Lake] modulo [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profiles.dataset.recordsuccess.count | Numero di record scritti nella propria origine dati da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profiles.dataset.recordfailed.count | Numero di record non riusciti da [!DNL Profile], per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profiles.dataset.batchsuccess.count | Numero di [!DNL Profile] batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profiles.dataset.batchfailed.count | Numero di [!DNL Profile] batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| platform.ups.ingest.streaming.request.m1_rate | Tasso richieste in arrivo. | Organizzazione IMS |
| platform.ups.ingest.streaming.access.put.success.m1_rate | Tasso di successo dell&#39;ingestione. | Organizzazione IMS |
| platform.ups.ingest.streaming.records.created.m15_rate | Frequenza dei nuovi record acquisiti per un set di dati. | ID set di dati |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | Frequenza dei record con marca temporale fuori ordine per la creazione di richieste per un dataset. | ID set di dati |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | Timestamp dell&#39;ultima richiesta di creazione record per un dataset. | ID set di dati |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | Frequenza dei record con marca temporale fuori ordine per la richiesta di aggiornamento per un dataset. | ID set di dati |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | Timestamp per l&#39;ultima richiesta di aggiornamento record per un dataset. | ID set di dati |
| platform.ups.ingest.streaming.record.size.m1_rate | Dimensione media del record. | Organizzazione IMS |
| platform.ups.ingest.streaming.records.updated.m15_rate | Frequenza delle richieste di aggiornamento per i record acquisiti per un set di dati. | ID set di dati |
