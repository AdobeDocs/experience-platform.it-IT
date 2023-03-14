---
audience: user
user-guide-title: Guida all’acquisizione dei dati di Adobe Experience Platform
breadcrumb-title: Guida all’acquisizione dei dati
user-guide-description: Trasmetti i dati a Experience Platform tramite l’acquisizione in batch o in streaming.
feature: Data Ingestion
source-git-commit: f77bbc60f2bc1f12970e8050ec6a924b9713f303
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 28%

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
   - Mappare un file CSV su XDM {#map-csv}
      - [Panoramica](./tutorials/map-csv/overview.md)
      - [Mappare un file CSV su uno schema esistente](./tutorials/map-csv/existing-schema.md)
      - [Mappare un file CSV utilizzando i consigli generati dall’intelligenza artificiale](./tutorials/map-csv/recommendations.md)
   - [Acquisire dati batch tramite l’interfaccia utente](tutorials/ingest-batch-data.md)
   - [Creare una connessione streaming autenticata](tutorials/create-authenticated-streaming-connection.md)
   - [Creare una connessione in streaming (API)](tutorials/create-streaming-connection.md)
   - [Creare una connessione in streaming (interfaccia utente)](tutorials/create-streaming-connection-ui.md)
   - [Trasmissione dei dati dei record](tutorials/streaming-record-data.md)
   - [Streaming di dati di serie temporali](tutorials/streaming-time-series-data.md)
   - [Trasmissione di più messaggi](tutorials/streaming-multiple-messages.md)
- Qualità dei dati e monitoraggio{#quality}
   - [Panoramica](quality/overview.md)
   - [Monitoraggio dell’acquisizione di dati](quality/monitor-data-ingestion.md)
   - [Recupera diagnostica degli errori](quality/error-diagnostics.md)
   - [Recupera batch non riusciti](quality/retrieve-failed-batches.md)
   - [Convalida acquisizione in streaming](quality/streaming-validation.md)
   - [Notifiche di acquisizione dei dati](quality/subscribe-events.md)
- [Guardrail per l’acquisizione dei dati](guardrails.md)
- [Connettori di origine](source-connectors.md)
- [Riferimento API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)
- [Note sulla versione della piattaforma](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=it)
