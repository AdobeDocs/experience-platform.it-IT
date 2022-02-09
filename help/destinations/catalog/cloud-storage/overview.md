---
keywords: destinazione di archiviazione cloud;archiviazione cloud
title: Panoramica delle destinazioni di archiviazione cloud
description: Adobe Experience Platform può fornire i segmenti come file di dati alle posizioni di archiviazione cloud di Amazon S3, AWS Kinesis, Azure Event Hubs o SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 818c9a6f5cd39db1405827b657872b99254ad1e5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Panoramica delle destinazioni di archiviazione cloud {#cloud-storage-destinations}

## Panoramica {#overview}

Adobe Experience Platform può distribuire i segmenti come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni tramite file CSV per [!DNL Amazon S3], [!DNL Azure Blob] e SFTP. Per [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs] destinazioni, i dati vengono inviati in streaming fuori Experience Platform in [!DNL JSON] formato.

![Destinazioni di Adobe per l’archiviazione cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinazioni di archiviazione cloud supportate {#supported-destinations}

Adobe Experience Platform supporta le seguenti destinazioni di archiviazione cloud:

* [Connessione Amazon Kinesis](amazon-kinesis.md)
* [Connessione Amazon S3](amazon-s3.md)
* [Connessione BLOB di Azure](azure-blob.md)
* [Connessione hub eventi di Azure](azure-event-hubs.md)
* [Connessione SFTP](sftp.md)

## Connessione a una nuova destinazione di archiviazione cloud {#connect-destination}

Per inviare segmenti alle destinazioni di archiviazione cloud per le campagne, Platform deve prima connettersi alla destinazione. Consulta la sezione [esercitazione sulla creazione di una destinazione](../../ui/connect-destination.md) informazioni dettagliate sulla configurazione di una nuova destinazione.


## Utilizzare le macro per creare una cartella nel percorso di archiviazione {#use-macros}

>[!NOTE]
>
> La funzionalità descritta in questa sezione è attualmente disponibile per [Amazon S3](amazon-s3.md) solo destinazioni.

Per creare una cartella personalizzata per ciascun file di segmento nel percorso di archiviazione, è possibile utilizzare le macro nel campo di immissione del percorso della cartella. Inserire le macro alla fine del campo di input, come illustrato di seguito.

![Come utilizzare le macro per creare una cartella nell&#39;archivio](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Gli esempi seguenti fanno riferimento a un segmento di esempio `Luxury Audience` con ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Ingresso: `acme/campaigns/2021/%SEGMENT_NAME%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Ingresso: `acme/campaigns/2021/%SEGMENT_ID%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Ingresso: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Tipo di esportazione dei dati {#export-type}

Supporto delle destinazioni di archiviazione cloud **Esportazione basata su profilo**. Questo significa che stai esportando i dettagli sui singoli utenti nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze a segmenti e altro ancora.