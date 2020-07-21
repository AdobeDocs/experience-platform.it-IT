---
title: Destinazione Amazon S3
seo-title: Destinazione Amazon S3
description: Crea una connessione live in uscita con l'archiviazione Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.
seo-description: Crea una connessione live in uscita con l'archiviazione Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# [!DNL Amazon S3] destinazione

## Panoramica

Crea una connessione in uscita dal vivo con l&#39;archivio S3 [!DNL Amazon Web Services] (AWS) per esportare periodicamente file di dati CSV o delimitati da tabulazioni da  Adobe Experience Platform nei tuoi bucket S3.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, comprese [!DNL Amazon S3]le destinazioni.

Per [!DNL Amazon S3] le destinazioni, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

* **[!DNL Amazon S3]chiave di accesso e chiave[!DNL Amazon S3]**segreta: In[!DNL Amazon S3], generate una coppia chiave di accesso - chiave di accesso segreta per consentire ad Adobe Real-time CDP di accedere al vostro[!DNL Amazon S3]account.



>[!IMPORTANT]
>
>Adobe Real-time CDP necessita di autorizzazioni `write` sull&#39;oggetto bucket in cui verranno inviati i file di esportazione.
