---
keywords: destinazione di archiviazione cloud;archiviazione cloud
title: Panoramica delle destinazioni di archiviazione cloud
description: Adobe Experience Platform può fornire i segmenti come file di dati alle posizioni di archiviazione cloud di Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Panoramica delle destinazioni di archiviazione cloud {#cloud-storage-destinations}

Adobe Experience Platform può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni tramite file CSV o file delimitati da tabulazioni per [!DNL Amazon S3], [!DNL Azure Blob] e SFTP. Per le destinazioni [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs], i dati vengono trasmessi in streaming in formato JSON.

![Destinazioni di Adobe per l’archiviazione cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Per informazioni su come connettersi alle destinazioni di archiviazione cloud, consulta [Flusso di lavoro per creare destinazioni di archiviazione cloud](./workflow.md).

## Tipo di esportazione dei dati

**Esportazione basata su profilo** : stai esportando i dettagli dei singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze a segmenti e altro ancora.

## Destinazioni di archiviazione cloud disponibili

- [Connessione Amazon S3](./amazon-s3.md)
- [Connessione BLOB di Azure](./azure-blob.md)
- [Connessione SFTP](./sftp.md)

## Destinazioni di streaming disponibili per l’archiviazione cloud

- [Connessione Amazon Kinesis](./amazon-kinesis.md)
- [Connessione hub eventi di Azure](./azure-event-hubs.md)