---
keywords: ' destinazione Amazon S3;S3;s3;amazon s3'
title: ' destinazione Amazon S3'
seo-title: ' destinazione Amazon S3'
description: Crea una connessione in uscita diretta con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
seo-description: Crea una connessione in uscita diretta con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Amazon S3] destinazione

## Panoramica

Crea una connessione in uscita dal vivo con l&#39;archivio [!DNL Amazon Web Services] (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.

## Tipo di esportazione {#export-type}

**Basato**  su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

![ tipo di esportazione basato su profilo Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destinazione Connect {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso [!DNL Amazon S3], vedere [Flusso di lavoro delle destinazioni di archiviazione cloud ](./workflow.md).

Per le destinazioni [!DNL Amazon S3], immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

* **[!DNL Amazon S3]chiave di accesso e chiave [!DNL Amazon S3]** segreta: In  [!DNL Amazon S3], generate una  `access key - secret access key` coppia per concedere l&#39;accesso Piattaforma al vostro  [!DNL Amazon S3] account. Ulteriori informazioni sono disponibili nella [ documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>La piattaforma necessita di autorizzazioni `write` sull&#39;oggetto bucket in cui verranno inviati i file di esportazione.

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Amazon S3], Platform crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [Destinazioni di marketing e archiviazione di e-mail e Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell&#39;esercitazione sull&#39;attivazione dei segmenti.
