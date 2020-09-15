---
product: experience-platform
audience: user
user-guide-title: Guida all'inserimento dei dati Adobe Experience Platform
breadcrumb-title: Data Ingestion Guide
user-guide-description: Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Platform services.
translation-type: tm+mt
source-git-commit: 2a5d6a9462950007d00f321ca9f3a3c457a3243e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [Panoramica sull&#39;inserimento dei dati](home.md)
- Caricamento in streaming {#streaming}
   - [Panoramica](streaming-ingestion/overview.md)
   - [Connettore Kafka](streaming-ingestion/kafka.md)
   - [Risoluzione dei problemi](streaming-ingestion/troubleshooting.md)
- Caricamento batch{#batch}
   - [Panoramica](batch-ingestion/overview.md)
   - [API di acquisizione batch](batch-ingestion/api-overview.md)
   - [Iniezione parziale del batch](batch-ingestion/partial.md)
   - [Risoluzione dei problemi](batch-ingestion/troubleshooting.md)
- Tutorial {#tutorials}
   - [Mappare un file CSV in XDM](tutorials/map-a-csv-file.md)
   - [Caricamento di dati batch tramite l’interfaccia utente](tutorials/ingest-batch-data.md)
   - [Creare una connessione in streaming autenticata](tutorials/create-authenticated-streaming-connection.md)
   - [Creare una connessione in streaming (API)](tutorials/create-streaming-connection.md)
   - [Creare una connessione in streaming (interfaccia utente)](tutorials/create-streaming-connection-ui.md)
   - [Streaming dei dati dei record](tutorials/streaming-record-data.md)
   - [Streaming dei dati delle serie temporali](tutorials/streaming-time-series-data.md)
   - [Streaming di più messaggi](tutorials/streaming-multiple-messages.md)
- Qualità e monitoraggio dell&#39;acquisizione dei dati{#quality}
   - [Panoramica](quality/overview.md)
   - [Monitorare i flussi di dati](quality/monitor-data-flows.md)
   - [Recupero della diagnostica degli errori](quality/error-diagnostics.md)
   - [Recupero batch non riusciti](quality/retrieve-failed-batches.md)
   - [Convalida dell&#39;assimilazione in streaming](quality/streaming-validation.md)
   - [Iscrizione agli eventi di assimilazione dei dati](quality/subscribe-events.md)
- [Connettori sorgente](source-connectors.md)
- [Riferimento API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Note sulla versione della piattaforma](https://www.adobe.com/go/platform-release-notes-en)