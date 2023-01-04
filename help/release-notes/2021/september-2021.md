---
title: Note sulla versione di Adobe Experience Platform - Settembre 2021
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

L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi in base ai quali Platform acquisisce i dati da varie sorgenti, nonché il modo in cui tali dati vengono mantenuti all’interno del Data Lake e possono essere utilizzati dai servizi di Platform a valle.

**Nuove funzioni**

| Funzione | Descrizione |
|------- | -----------|
| Aggiornare o applicare patch i record del profilo utilizzando l’acquisizione batch | Il profilo cliente in tempo reale ora consente di aggiornare gli attributi del profilo nei dati dei record dei singoli profili tramite l’acquisizione batch. Per ulteriori informazioni, consulta la sezione [guida per gli sviluppatori di batch ingestion](../../ingestion/batch-ingestion/api-overview.md). |

Per ulteriori informazioni sull’acquisizione di dati in Platform, visita la pagina [Documentazione sull’acquisizione dei dati](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto per flussi di dati in streaming | È ora possibile utilizzare le funzioni di preparazione dei dati durante la creazione di un flusso di dati per [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]e [!DNL Google PubSub]. Guarda l’esercitazione su [creazione di un flusso di dati in streaming per le origini di archiviazione cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) per ulteriori informazioni. |

Per ulteriori informazioni [!DNL Data Prep] vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Data Landing Zone] | Ora puoi creare una [!DNL Data Landing Zone] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o [interfaccia utente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] è un [!DNL Azure Blob] l’interfaccia di archiviazione fornita da Platform ti consente di accedere a una struttura di archiviazione file sicura basata su cloud per l’importazione di file in Platform. Consulta la sezione [[!DNL Data Landing Zone] panoramica](../../sources/connectors/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |
| [!DNL Snowflake] | Ora puoi creare una [!DNL Snowflake] connessione di origine tramite [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o [interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md) per ottenere i dati dal [!DNL Snowflake] database su Platform. Consulta la sezione [[!DNL Snowflake] panoramica](../../sources/connectors/databases/snowflake.md) per ulteriori informazioni. |
| [!DNL SFTP] miglioramenti alla sorgente | Puoi impostare manualmente un numero di porta personalizzato durante la creazione di un [!DNL SFTP] connessione di origine. Consulta la sezione [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
