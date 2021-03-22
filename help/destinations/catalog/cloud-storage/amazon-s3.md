---
keywords: Amazon S3;destinazione S3;s3;amazon s3
title: Connessione Amazon S3
description: Crea una connessione in uscita diretta all’archiviazione S3 di Amazon Web Services (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei bucket S3.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '223'
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

>[!IMPORTANT]
>
>Platform necessita di autorizzazioni `write` sull’oggetto bucket in cui verranno consegnati i file di esportazione.

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Amazon S3], Platform crea un file `.txt` o `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.
