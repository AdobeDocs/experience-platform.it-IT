---
keywords: Amazon S3;destinazione S3;s3;amazon s3
title: Connessione Amazon S3
description: Crea una connessione in uscita diretta all’archiviazione S3 di Amazon Web Services (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei bucket S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Panoramica {#overview}

Crea una connessione in uscita dal vivo all’archiviazione S3 [!DNL Amazon Web Services] (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei bucket S3.

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!DNL Amazon S3]chiave** di accesso e chiave  **[!DNL Amazon S3]segreta**: In  [!DNL Amazon S3], genera una  `access key - secret access key` coppia per concedere a Platform l’accesso al tuo  [!DNL Amazon S3] account. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Nome]** blocco: immetti il nome del  [!DNL Amazon S3] bucket da utilizzare per la destinazione.
* **[!UICONTROL Percorso]** cartella: immetti il percorso della cartella di destinazione che ospiterà i file esportati.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

>[!TIP]
>
>Nel flusso di lavoro di destinazione di connessione puoi creare una cartella personalizzata nell’archivio Amazon S3 per file di segmento esportato. Per istruzioni, leggere [Utilizzare le macro per creare una cartella nel percorso di archiviazione](overview.md#use-macros).

### Autorizzazioni [!DNL Amazon S3] necessarie {#required-s3-permission}

Per connettere ed esportare correttamente i dati nel percorso di archiviazione [!DNL Amazon S3], crea un utente IAM (Identity and Access Management) per [!DNL Platform] in [!DNL Amazon S3] e assegna le autorizzazioni per le azioni seguenti:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico nelle destinazioni, consulta [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md) .

## Dati esportati {#exported-data}

Per le destinazioni [!DNL Amazon S3], [!DNL Platform] crea un file `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.
