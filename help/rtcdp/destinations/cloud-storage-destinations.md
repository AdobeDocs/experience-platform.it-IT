---
title: Destinazioni di archiviazione cloud
seo-title: Destinazioni di archiviazione cloud
description: Adobe Real-time CDP può inviare i segmenti come file di dati alle posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
seo-description: Adobe Real-time CDP può inviare i segmenti come file di dati alle posizioni di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Destinazioni di archiviazione cloud {#cloud-storage-destinations}

Adobe Real-time CDP può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare audience e i relativi attributi di profilo ai sistemi interni, tramite file CSV o delimitati da tabulazioni per [!DNL Amazon S3] e SFTP. Per [!DNL AWS Kinesis] e [!DNL Azure Event Hubs] le destinazioni, i dati vengono inviati in streaming da  Experience Platform in formato JSON.

![Destinazioni di archiviazione di Adobe Cloud](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Per informazioni su come connettersi alle destinazioni di archiviazione cloud, vedi [Flusso di lavoro per creare destinazioni](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)di archiviazione cloud.

## Tipo esportazione dati

**Esportazione** basata su profilo: state esportando i dettagli dei singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze ai segmenti, ecc.

## Destinazioni di archiviazione cloud disponibili

* [Destinazione Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md)
* [Destinazione SFTP](/help/rtcdp/destinations/sftp-destination.md)

## Destinazioni di streaming per l&#39;archiviazione cloud disponibili

* [destinazione Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Destinazione Hubs evento Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)