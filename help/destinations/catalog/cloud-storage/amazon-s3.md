---
keywords: Amazon S3;destinazione S3;s3;amazon s3
title: Connessione Amazon S3
description: Crea una connessione in uscita diretta all’archiviazione S3 di Amazon Web Services (AWS) per esportare periodicamente file di dati CSV da Adobe Experience Platform nei bucket S3.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Panoramica {#overview}

Crea una connessione in uscita diretta al tuo [!DNL Amazon Web Services] (AWS) Archiviazione S3 per esportare periodicamente file di dati CSV da Adobe Experience Platform nei bucket S3.

## Tipo di esportazione {#export-type}

**Basato su profilo** - si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata Seleziona attributi del [flusso di lavoro di attivazione della destinazione](../../ui/activate-segment-streaming-destinations.md#mapping).

![Tipo di esportazione basato su profilo Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!DNL Amazon S3]chiave di accesso** e **[!DNL Amazon S3]chiave segreta**: In [!DNL Amazon S3], genera un `access key - secret access key` per concedere a Platform l’accesso al tuo [!DNL Amazon S3] conto. Ulteriori informazioni nel [Documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Nome blocco]**: immetti il nome della [!DNL Amazon S3] bucket utilizzato da questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.

>[!TIP]
>
>Nel flusso di lavoro di destinazione di connessione puoi creare una cartella personalizzata nell’archivio Amazon S3 per file di segmento esportato. Leggi [Utilizzare le macro per creare una cartella nel percorso di archiviazione](overview.md#use-macros) per istruzioni.

### Obbligatorio [!DNL Amazon S3] permissions {#required-s3-permission}

Per connettere ed esportare correttamente i dati al tuo [!DNL Amazon S3] posizione di archiviazione, creare un utente IAM (Identity and Access Management) per [!DNL Platform] in [!DNL Amazon S3] e assegna le autorizzazioni per le azioni seguenti:

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

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Per [!DNL Amazon S3] destinazioni, [!DNL Platform] crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) nell’esercitazione sull’attivazione dei segmenti.
