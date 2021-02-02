---
keywords: destinazione di archiviazione cloud;archiviazione cloud
title: Destinazioni di archiviazione cloud
seo-title: Destinazioni di archiviazione cloud
description: La piattaforma può distribuire i segmenti come file di dati alle  posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
seo-description: La piattaforma può distribuire i segmenti come file di dati alle  posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: b348a5493b13112291dd8e9234d457ff8c694147
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Destinazioni di archiviazione cloud {#cloud-storage-destinations}

Adobe Experience Platform può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare audience e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni per [!DNL Amazon S3] e SFTP. Per le destinazioni [!DNL AWS Kinesis] e [!DNL Azure Event Hubs], i dati vengono inviati in streaming  Experience Platform in formato JSON.

![ destinazioni di archiviazione cloud Adobe](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Per informazioni su come connettersi alle destinazioni di archiviazione cloud, vedere [Flusso di lavoro per creare le destinazioni di archiviazione cloud](./workflow.md).

## Tipo esportazione dati

**Esportazione**  basata su profilo: state esportando i dettagli relativi ai singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze ai segmenti, ecc.

## Destinazioni di archiviazione cloud disponibili

- [ destinazione Amazon S3](./amazon-s3.md)
- [Destinazione BLOB di Azure](./azure-blob.md)
- [Destinazione SFTP](./sftp.md)

## Destinazioni di streaming di archiviazione cloud disponibili

- [ destinazione Amazon Kinesis](./amazon-kinesis.md)
- [Destinazione Hubs evento Azure](./azure-event-hubs.md)