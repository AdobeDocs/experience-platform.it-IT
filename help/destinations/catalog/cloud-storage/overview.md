---
keywords: cloud storage destination;cloud storage
title: Destinazioni di archiviazione cloud
seo-title: Destinazioni di archiviazione cloud
description: CDP in tempo reale può distribuire i segmenti come file di dati alle  posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
seo-description: CDP in tempo reale può distribuire i segmenti come file di dati alle  posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Destinazioni di archiviazione cloud {#cloud-storage-destinations}

CDP in tempo reale può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare audience e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni per [!DNL Amazon S3] e SFTP. Per [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] le destinazioni, i dati vengono inviati in streaming  Experience Platform in formato JSON.

![destinazioni di archiviazione cloud di Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Per informazioni su come connettersi alle destinazioni di archiviazione cloud, vedi [Flusso di lavoro per creare destinazioni](./workflow.md)di archiviazione cloud.

## Tipo esportazione dati

**Esportazione** basata su profilo: state esportando i dettagli dei singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze ai segmenti, ecc.

## Destinazioni di archiviazione cloud disponibili

- [destinazione Amazon S3](./amazon-s3.md)
- [Destinazione SFTP](./sftp.md)

## Destinazioni di streaming per l&#39;archiviazione cloud disponibili

- [destinazione Amazon Kinesis](./amazon-kinesis.md)
- [Destinazione Hubs evento Azure](./azure-event-hubs.md)