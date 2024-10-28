---
keywords: destinazione archiviazione cloud;archiviazione cloud
title: Panoramica delle destinazioni di archiviazione cloud
description: Adobe Experience Platform può distribuire i tipi di pubblico come file di dati ai percorsi di archiviazione cloud Amazon S3, AWS Kinesis, Azure Event Hub o SFTP.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 2e21e62de624c5e7e9fac4d36dbf41b46198062a
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 5%

---

# Panoramica delle destinazioni dell’archiviazione cloud {#cloud-storage-destinations}

## Panoramica {#overview}

Adobe Experience Platform può distribuire i tipi di pubblico come file di dati alle posizioni di archiviazione cloud. Questo consente di inviare i tipi di pubblico e i relativi attributi di profilo ai sistemi interni, tramite file CSV per [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] e SFTP. Per le destinazioni [!DNL Amazon Kinesis] e [!DNL Azure Event Hubs], i dati vengono inviati in streaming dall&#39;Experience Platform in formato [!DNL JSON].

![Destinazioni Adobi di archiviazione cloud](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Destinazioni di archiviazione cloud supportate {#supported-destinations}

Adobe Experience Platform supporta le esportazioni di dati verso le seguenti destinazioni di archiviazione cloud:

* [Connessione Amazon Kinesis](amazon-kinesis.md)
* [Connessione Amazon S3](amazon-s3.md)
* [Connessione BLOB di Azure](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Connessione Azure Event Hubs](azure-event-hubs.md)
* [Data Landing Zone](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [Connessione SFTP](sftp.md)

## Connettersi a una nuova destinazione di archiviazione cloud {#connect-destination}

Per inviare i tipi di pubblico alle destinazioni di archiviazione cloud per le campagne, Platform deve prima connettersi alla destinazione. Per informazioni dettagliate sulla configurazione di una nuova destinazione, consulta il [tutorial sulla creazione della destinazione](../../ui/connect-destination.md).


## Utilizzare le macro per creare una cartella nel percorso di archiviazione {#use-macros}

>[!NOTE]
>
> La funzionalità descritta in questa sezione è disponibile per tutte le destinazioni di archiviazione cloud. Tuttavia, la destinazione [Amazon S3](amazon-s3.md) supporta attualmente solo le macro `%SEGMENT_ID%` e `%SEGMENT_NAME%`.

Per creare una cartella personalizzata per file di pubblico nel percorso di archiviazione, puoi utilizzare le macro nel campo di input del percorso della cartella. Inserire le macro alla fine del campo di input, come illustrato di seguito.

![Come utilizzare le macro per creare una cartella nell&#39;archivio](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Gli esempi seguenti fanno riferimento a un pubblico di esempio `Luxury Audience` con ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Macro 1:`%SEGMENT_NAME%`**

Input: `acme/campaigns/2021/%SEGMENT_NAME%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience`

**Macro 2:`%SEGMENT_ID%`**

Input: `acme/campaigns/2021/%SEGMENT_ID%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Macro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Input: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Percorso cartella nel percorso di archiviazione: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Altre macro**

Analogamente agli esempi precedenti, è possibile utilizzare ulteriori macro per creare una struttura di cartelle personalizzata nel percorso della cartella:

* `%DATETIME%` o `%TIMESTAMP%` per aggiungere un nome di cartella personalizzato in base al tempo di esportazione dei file. Il formato per la prima macro è `MMDDYYYY_HHMMSS` e il formato UNIX a 10 cifre per la seconda macro.
* `%DESTINATION_NAME%` per aggiungere una cartella personalizzata in base al nome del flusso di dati di destinazione.

## Tipo di esportazione dei dati {#export-type}

Le destinazioni di archiviazione cloud supportano i seguenti tipi di esportazione:
* **Esportazione basata su profilo**. Ciò significa che stai esportando dettagli sulle persone nel pubblico. Questi dettagli sono necessari per la personalizzazione e possono includere attributi, eventi, appartenenze a un pubblico e altro ancora.
* **Esportazione set di dati**. Questa funzionalità consente di esportare interi set di dati in destinazioni di archiviazione cloud. [Ulteriori informazioni](/help/destinations/ui/export-datasets.md) sulla funzionalità.

## Passaggi successivi {#next-steps}

Dopo aver selezionato una delle [destinazioni cloud supportate](#supported-destinations) da utilizzare, leggere l&#39;esercitazione [connetti a destinazioni](/help/destinations/ui/connect-destination.md) per scoprire come stabilire una connessione alla destinazione. Quindi, leggi il tutorial di attivazione sulle destinazioni basate su file per scoprire come avviare l&#39;esportazione dei dati di [1} nella destinazione dell&#39;archiviazione cloud.](/help/destinations/ui/activate-batch-profile-destinations.md)
