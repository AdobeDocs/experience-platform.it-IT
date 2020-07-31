---
title: ' destinazione Amazon S3'
seo-title: ' destinazione Amazon S3'
description: Crea una connessione live in uscita con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.
seo-description: Crea una connessione live in uscita con l'archivio  Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# [!DNL Amazon S3] destinazione

## Panoramica

Crea una connessione in uscita dal vivo con l&#39;archivio S3 [!DNL Amazon Web Services] (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, comprese [!DNL Amazon S3]le destinazioni.

Per [!DNL Amazon S3] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

* **[!DNL Amazon S3]chiave di accesso e chiave[!DNL Amazon S3]**segreta: In[!DNL Amazon S3], generate una coppia di chiavi di accesso - chiave di accesso segreta per concedere al Adobe l&#39;accesso CDP in tempo reale al vostro[!DNL Amazon S3]account.

>[!IMPORTANT]
>
> Adobe CDP in tempo reale richiede `write` le autorizzazioni per l&#39;oggetto bucket in cui verranno inviati i file di esportazione.

## Dati esportati {#exported-data}

Per [!DNL Amazon S3] le destinazioni,  Adobe CDP in tempo reale crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
