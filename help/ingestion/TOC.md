---
audience: user
user-guide-title: Guida all’acquisizione dei dati di Adobe Experience Platform
breadcrumb-title: Guida all’acquisizione dei dati
user-guide-description: Trasmetti i dati a Experience Platform tramite l’acquisizione in batch o in streaming.
feature: Data Ingestion
source-git-commit: 6110bf51cbd0005428e7dab4552944c5c9b54d03
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 26%

---


# Acquisizione dei dati Adobe Experience Platform {#ingestion}

- [Panoramica sull’acquisizione dei dati](home.md)
- Acquisizione in streaming {#streaming}
   - [Panoramica](streaming-ingestion/overview.md)
   - [Connettore Kafka](streaming-ingestion/kafka.md)
   - [Risoluzione dei problemi](streaming-ingestion/troubleshooting.md)
- Acquisizione batch{#batch}
   - [Guida introduttiva alle API di acquisizione batch](batch-ingestion/getting-started.md)
   - [Panoramica API](batch-ingestion/overview.md)
   - [Guida per gli sviluppatori API](batch-ingestion/api-overview.md)
   - [Acquisizione batch parziale](batch-ingestion/partial.md)
   - [Risoluzione dei problemi](batch-ingestion/troubleshooting.md)
- Tutorial {#tutorials}
   - Mappare un file CSV in XDM {#map-csv}
      - [Panoramica](./tutorials/map-csv/overview.md)
      - [Mappare un file CSV su uno schema esistente](./tutorials/map-csv/existing-schema.md)
      - [Mappare un file CSV utilizzando i consigli generati dall&#39;intelligenza artificiale](./tutorials/map-csv/recommendations.md)
   - [Inserire dati batch tramite l’interfaccia utente](tutorials/ingest-batch-data.md)
   - [Creare una connessione in streaming autenticata](tutorials/create-authenticated-streaming-connection.md)
   - [Creare una connessione in streaming (API)](tutorials/create-streaming-connection.md)
   - [Creare una connessione in streaming (interfaccia utente)](tutorials/create-streaming-connection-ui.md)
   - [Dati record in streaming](tutorials/streaming-record-data.md)
   - [Dati delle serie temporali in streaming](tutorials/streaming-time-series-data.md)
   - [Streaming di più messaggi](tutorials/streaming-multiple-messages.md)
- Qualità e monitoraggio dei dati{#quality}
   - [Panoramica](quality/overview.md)
   - [Monitoraggio dell’acquisizione di dati](quality/monitor-data-ingestion.md)
   - [Recupera diagnostica errori](quality/error-diagnostics.md)
   - [Recupera batch non riusciti](quality/retrieve-failed-batches.md)
   - [Convalida dell’acquisizione in streaming](quality/streaming-validation.md)
   - [Notifiche di acquisizione dei dati](quality/subscribe-events.md)
- [Guardrail per l’inserimento dei dati](guardrails.md)
- [Connettori di origine](source-connectors.md)
- [Riferimento API per l’acquisizione in batch](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [Riferimento API per l’acquisizione in streaming](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Note sulla versione di Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=it)
