---
keywords: destinazione di archiviazione cloud;archiviazione cloud
title: Panoramica delle destinazioni di archiviazione cloud
description: Adobe Experience Platform può distribuire i segmenti come file di dati alle  posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Panoramica delle destinazioni di archiviazione cloud {#cloud-storage-destinations}

Adobe Experience Platform può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare audience e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni per [!DNL Amazon S3] e SFTP. Per le destinazioni [!DNL AWS Kinesis] e [!DNL Azure Event Hubs], i dati vengono inviati in streaming  Experience Platform in formato JSON.

![ destinazioni di archiviazione cloud Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Per informazioni su come connettersi alle destinazioni di archiviazione cloud, vedere [Flusso di lavoro per creare le destinazioni di archiviazione cloud](./workflow.md).

## Tipo esportazione dati

**Esportazione**  basata su profilo: state esportando i dettagli relativi ai singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze ai segmenti, ecc.

## Destinazioni di archiviazione cloud disponibili

- [ connessione Amazon S3](./amazon-s3.md)
- [Connessione BLOB di Azure](./azure-blob.md)
- [Connessione SFTP](./sftp.md)

## Destinazioni di streaming di archiviazione cloud disponibili

- [ connessione Amazon Kinesis](./amazon-kinesis.md)
- [Connessione Hubs evento di Azure](./azure-event-hubs.md)