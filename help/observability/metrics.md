---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metriche disponibili
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# Elenco delle metriche disponibili

Di seguito è riportato un elenco di metriche esposte da Observability Insights, ognuna con il relativo servizio Piattaforma, descrizione e parametro di query ID accettato.

| Metrica Insights | Servizio piattaforma | Descrizione | Parametro query ID |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | Ingestione dati | Numero totale di set di dati creati. | N/D |
| timeseries.ingestion.dataset.size | Ingestione dati | Dimensione cumulativa di tutti i dati acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.dailysize | Ingestione dati | Dimensione dei dati acquisiti su base giornaliera per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.batchFailed.count | Ingestione dati | Numero di batch non riusciti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.batchsuccess.count | Ingestione dati | Numero di batch acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.ingestion.dataset.record.success.count | Ingestione dati | Numero di record acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.total.messages.rate | Ingestione dati (streaming) | Numero totale di messaggi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.valid.messages.rate | Ingestione dati (streaming) | Numero totale di messaggi validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.Invalid.messages.rate | Ingestione dati (streaming) | Numero totale di messaggi non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.type.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;tipo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.range.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;intervallo&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.format.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;formato&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.pattern.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;pattern&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.presence.count | Ingestione dati (streaming) | Numero totale di messaggi di &quot;presenza&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.enum.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;enum&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.unlassificati.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;non classificati&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.validation.category.unknown.count | Ingestione dati (streaming) | Numero totale di messaggi &quot;sconosciuti&quot; non validi per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.data.collection.inlet.total.messages.Received | Ingestione dati (streaming) | Numero totale di messaggi ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso (facoltativo) |
| timeseries.data.collection.inlet.total.messages.size.Received | Ingestione dati (streaming) | Dimensione totale dei dati ricevuti per una entrata dati o per tutte le ingressi di dati. | ID ingresso (facoltativo) |
| timeseries.data.collection.inlet.success | Ingestione dati (streaming) | Numero totale di chiamate HTTP riuscite a un&#39;entrata dati o a tutte le insenature dati. | ID ingresso (facoltativo) |
| timeseries.data.collection.inlet.failure | Ingestione dati (streaming) | Numero totale di chiamate HTTP non riuscite a una entrata dati o a tutte le insenature dati. | ID ingresso (facoltativo) |
| timeseries.profile.dataset.record.count | Profilo cliente in tempo reale | Numero di record letti dal lago di dati per profilo, per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profile.dataset.record.success.count | Profilo cliente in tempo reale | Numero di record scritti nella propria origine dati da Profilo, per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profile.dataset.record.fail.count | Profilo cliente in tempo reale | Numero di record non riusciti da Profilo, per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profile.dataset.batchsuccess.count | Profilo cliente in tempo reale | Numero di batch di profili acquisiti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.profile.dataset.batchFailed.count | Profilo cliente in tempo reale | Numero di batch di profili non riusciti per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.identity.dataset.record.success.count | Servizio identità | Numero di record scritti nell&#39;origine dati da Servizio identità per un set di dati o tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.identity.dataset.record.fail.count | Servizio identità | Numero di record non riusciti dal servizio identità, per un set di dati o per tutti i set di dati. | ID set di dati (facoltativo) |
| timeseries.identity.dataset.namespacecode.record.success.count | Servizio identità | Numero di record di identità acquisiti correttamente per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.recordFailed.count | Servizio identità | Numero di record di identità non riuscito da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.dataset.namespacecode.record.skipped.count | Servizio identità | Numero di record di identità ignorati da uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | Servizio identità | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | Servizio identità | Numero di identità univoche memorizzate nel grafico dell&#39;identità per uno spazio dei nomi. | ID spazio nomi (**obbligatorio**) |
| timeseries.identity.graph.imsorg.numidgraph.count | Servizio identità | Numero di identità univoche del grafico memorizzate nel grafico di identità per l&#39;organizzazione IMS. | N/D |
| timeseries.identity.graph.imsorg.graphstrong.uniqueidentities.count | Servizio identità | Numero di identità univoche memorizzate nel grafico dell&#39;identità per l&#39;organizzazione IMS per una particolare intensità del grafico (&quot;sconosciuto&quot;, &quot;debole&quot; o &quot;forte&quot;). | Forza del grafico (**richiesta**) |
| timeseries.gdpr.Jobs.totaljobs.count | GDPR | Numero totale di posti di lavoro creati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.complete.count | GDPR | Numero totale di processi completati dal GDPR. | ENV (**obbligatorio**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR | Numero totale di processi di errore da GDPR. | ENV (**obbligatorio**) |
| timeseries.queryservice.query.scheduleonce.count | Servizio query | Numero totale di query pianificate non ricorrenti. | N/D |
| timeseries.queryservice.query.scheduledperiodico.count | Servizio query | Numero totale di query programmate ricorrenti. | N/D |
| timeseries.queryservice.query.batchquery.count | Servizio query | Numero totale di query batch eseguite. | N/D |
| timeseries.queryservice.query.scheduledquery.count | Servizio query | Numero totale di query pianificate eseguite. | N/D |
| timeseries.queryservice.query.interactivequery.count | Servizio query | Numero totale di query interattive eseguite. | N/D |
| timeseries.queryservice.query.batchfrompsqlquery.count | Servizio query | Numero totale di query batch eseguite da PSQL. | N/D |