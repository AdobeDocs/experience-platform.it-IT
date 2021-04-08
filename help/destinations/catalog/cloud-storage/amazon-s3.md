---
keywords: Amazon S3;destinazione S3;s3;amazon s3
title: Connessione Amazon S3
description: Crea una connessione in uscita diretta all’archiviazione S3 di Amazon Web Services (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei bucket S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
translation-type: tm+mt
source-git-commit: d77cd063e61118631b757d9821267b2fd6ab0148
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# [!DNL Amazon S3] connection  {#s3-connection}

## Panoramica {#overview}

Crea una connessione in uscita dal vivo all’archiviazione S3 [!DNL Amazon Web Services] (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei bucket S3.

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Collegare la destinazione {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, tra cui [!DNL Amazon S3], consulta [Flusso di lavoro delle destinazioni di archiviazione cloud ](./workflow.md) .

Per le destinazioni [!DNL Amazon S3] , inserisci le seguenti informazioni nel flusso di lavoro crea destinazione :

* **[!DNL Amazon S3]chiave di accesso e chiave  [!DNL Amazon S3] segreta**: In  [!DNL Amazon S3], genera una  `access key - secret access key` coppia per concedere a Platform l’accesso al tuo  [!DNL Amazon S3] account. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

## Autorizzazioni [!DNL Amazon S3] necessarie {#required-s3-permission}

Per connettere ed esportare correttamente i dati nel percorso di archiviazione [!DNL Amazon S3], crea un utente IAM per [!DNL Platform] in [!DNL Amazon S3] e assegna le autorizzazioni per le azioni seguenti:

* `s3:DeleteObject`
* `s3:DeleteObjectVersion`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:GetObjectVersion`
* `s3:ListBucket`
* `s3:ListBuckets`
* `s3:PutBucketVersioning`
* `s3:PutObject`
* `s3:ReplicateObject`
* `s3:RestoreObject`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Dati esportati {#exported-data}

Per le destinazioni [!DNL Amazon S3], [!DNL Platform] crea un file `.txt` o `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.
