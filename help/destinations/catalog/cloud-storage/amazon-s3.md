---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: ' destinazione Amazon S3'
seo-title: ' destinazione Amazon S3'
description: Crea una connessione in uscita diretta con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
seo-description: Crea una connessione in uscita diretta con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] destinazione

## Panoramica

Crea una connessione in uscita dal vivo con il tuo storage [!DNL Amazon Web Services] (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi socket S3.

## Tipo esportazione {#export-type}

**Basato** su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [di attivazione della](../../ui/activate-destinations.md#select-attributes)destinazione.

![tipo di esportazione basato su profilo Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](./workflow.md) per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso [!DNL Amazon S3]il

Per [!DNL Amazon S3] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

* **[!DNL Amazon S3]chiave di accesso e chiave [!DNL Amazon S3]** segreta: In [!DNL Amazon S3], generate una `access key - secret access key` coppia per consentire a CDP in tempo reale di accedere al vostro [!DNL Amazon S3] account. Ulteriori informazioni sono disponibili nella [documentazione](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)di Amazon Web Services.

>[!IMPORTANT]
>
>CDP in tempo reale richiede `write` autorizzazioni per l’oggetto bucket in cui verranno inviati i file di esportazione.

## Dati esportati {#exported-data}

Per [!DNL Amazon S3] le destinazioni, in Real-time CDP viene creato un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](../../ui/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.
