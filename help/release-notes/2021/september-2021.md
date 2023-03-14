---
title: Note sulla versione di Adobe Experience Platform di settembre 2021
description: Note sulla versione di settembre 2021 per Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 settembre 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Acquisizione dei dati](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Origini](#sources)

## Acquisizione dei dati {#ingestion}

L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi con cui Platform acquisisce i dati da varie origini, nonché il modo in cui tali dati vengono memorizzati nel Data Lake per l’utilizzo da parte dei servizi Platform a valle.

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Eseguire l’upsert o patch dei record del profilo tramite l’acquisizione in batch | Real-Time Customer Profile ora consente di aggiornare gli attributi del profilo nei dati dei singoli record di profilo tramite l’acquisizione batch. Per ulteriori informazioni, consulta [guida per gli sviluppatori sull’acquisizione batch](../../ingestion/batch-ingestion/api-overview.md). |

Per ulteriori informazioni sull’acquisizione di dati in Platform, visita [Documentazione sull’acquisizione dei dati](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per flussi di dati in streaming | È ora possibile utilizzare le funzioni di preparazione dei dati durante la creazione di un flusso di dati in streaming per [!DNL Amazon Kinesis], [!DNL Azure Event Hubs], e [!DNL Google PubSub]. Guarda il tutorial su [creazione di un flusso di dati in streaming per le origini di archiviazione cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) per ulteriori informazioni. |

Per ulteriori informazioni su [!DNL Data Prep] vedi la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Data Landing Zone] | Ora puoi creare una [!DNL Data Landing Zone] connessione sorgente tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o [interfaccia utente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] è un [!DNL Azure Blob] con il provisioning di Platform, ti consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per inserire i file in Platform. Consulta la [[!DNL Data Landing Zone] panoramica](../../sources/connectors/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |
| [!DNL Snowflake] | Ora puoi creare una [!DNL Snowflake] connessione sorgente tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o [interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md) per importare i dati dal [!DNL Snowflake] da database a Platform. Consulta la [[!DNL Snowflake] panoramica](../../sources/connectors/databases/snowflake.md) per ulteriori informazioni. |
| [!DNL SFTP] miglioramenti all&#39;origine | È possibile impostare manualmente un numero di porta personalizzato durante la creazione di un [!DNL SFTP] connessione sorgente. Consulta la [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
