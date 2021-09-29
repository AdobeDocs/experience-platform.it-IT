---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: b616a0c0d49d980644f82bc3af5995b3b17b4c80
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 12%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 settembre 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Fonti](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Supporto per flussi di dati in streaming | È ora possibile utilizzare le funzioni di preparazione dei dati durante la creazione di un flusso di dati per [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] e [!DNL Google PubSub]. Per ulteriori informazioni, consulta l’esercitazione su [creazione di un flusso di dati in streaming per le origini di archiviazione cloud](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) . |

Per ulteriori informazioni su [!DNL Data Prep], consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Fonti {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| [!DNL Data Landing Zone] | È ora possibile creare una connessione sorgente [!DNL Data Landing Zone] utilizzando l’ [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) o l’ [interfaccia utente](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] è un’interfaccia di  [!DNL Azure Blob] archiviazione fornita da Platform che consente di accedere a una struttura di storage basata su cloud sicura per l’acquisizione e l’uscita di file da e verso Platform. Per ulteriori informazioni, consulta la sezione [[!DNL Data Landing Zone] panoramica](../../sources/connectors/cloud-storage/data-landing-zone.md) . |
| [!DNL Snowflake] | È ora possibile creare una connessione sorgente [!DNL Snowflake] utilizzando [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) o l’ [interfaccia utente](../../sources/tutorials/ui/create/databases/snowflake.md) per trasferire i dati dal database [!DNL Snowflake] a Platform. Per ulteriori informazioni, consulta la sezione [[!DNL Snowflake] panoramica](../../sources/connectors/databases/snowflake.md) . |
| [!DNL SFTP] miglioramenti alla sorgente | Puoi impostare manualmente un numero di porta personalizzato durante la creazione di una connessione sorgente [!DNL SFTP]. Per ulteriori informazioni, consulta la sezione [[!DNL SFTP] panoramica](../../sources/connectors/cloud-storage/sftp.md) . |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
