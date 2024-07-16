---
title: Note sulla versione di Adobe Experience Platform di settembre 2021
description: Note sulla versione di settembre 2021 per Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 26%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 29 settembre 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Acquisizione dei dati](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [Origini](#sources)

## Acquisizione dei dati {#ingestion}

L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi con cui Platform acquisisce i dati da varie origini, nonché il modo in cui tali dati vengono memorizzati nel Data Lake per l’utilizzo da parte dei servizi Platform a valle.

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Eseguire l’upsert o patch dei record del profilo tramite l’acquisizione in batch | Real-Time Customer Profile ora consente di aggiornare gli attributi del profilo nei dati dei singoli record di profilo tramite l’acquisizione batch. Per ulteriori informazioni, consulta la [guida per gli sviluppatori per l&#39;acquisizione batch](../../ingestion/batch-ingestion/api-overview.md). |

Per ulteriori informazioni sull&#39;acquisizione di dati in Platform, consulta la [documentazione sull&#39;acquisizione dei dati](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per flussi di dati in streaming | È ora possibile utilizzare le funzioni di preparazione dati durante la creazione di un flusso di dati in streaming per [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] e [!DNL Google PubSub]. Per ulteriori informazioni, consulta l&#39;esercitazione su [creazione di un flusso di dati in streaming per le origini di archiviazione cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md). |

Per ulteriori informazioni su [!DNL Data Prep], consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Data Landing Zone] | È ora possibile creare una connessione di origine [!DNL Data Landing Zone] utilizzando [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o l&#39;interfaccia utente [4}. ](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) [!DNL Data Landing Zone] è un&#39;interfaccia di archiviazione [!DNL Azure Blob] fornita da Platform, che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per inserire i file in Platform. Per ulteriori informazioni, vedere [[!DNL Data Landing Zone] panoramica](../../sources/connectors/cloud-storage/data-landing-zone.md). |
| [!DNL Snowflake] | È ora possibile creare una connessione di origine [!DNL Snowflake] utilizzando l&#39;[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o l&#39;[interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md) per portare dati dal database [!DNL Snowflake] a Platform. Per ulteriori informazioni, vedere [[!DNL Snowflake] panoramica](../../sources/connectors/databases/snowflake.md). |
| [!DNL SFTP] miglioramenti all&#39;origine | È possibile impostare manualmente un numero di porta personalizzato durante la creazione di una connessione di origine [!DNL SFTP]. Per ulteriori informazioni, vedere [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md). |

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
