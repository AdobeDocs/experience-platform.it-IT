---
title: Destinazione Amazon S3
seo-title: Destinazione Amazon S3
description: Crea una connessione in uscita dal vivo con l'archiviazione Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
seo-description: Crea una connessione in uscita dal vivo con l'archiviazione Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.
translation-type: tm+mt
source-git-commit: acd3865be4994a478048d317060c55b7e0d9914c

---


# Destinazione Amazon S3

## Panoramica

Crea una connessione in uscita dal vivo con l&#39;archiviazione Amazon Web Services (AWS) S3 per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform nei tuoi bucket S3.

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso Amazon S3.

Per le destinazioni Amazon S3, immettete le seguenti informazioni nel flusso di lavoro di creazione della destinazione:

* **Chiave di accesso Amazon S3 e chiave** segreta Amazon S3: In Amazon S3, generate una coppia chiave di accesso segreta per consentire ad Adobe Real-time CDP di accedere al vostro account Amazon S3;
* **Percorso** Amazon S3: Si tratta della posizione nel bucket Amazon S3 in cui Adobe Real-time CDP distribuirà i file di esportazione.


>[!IMPORTANT]
>
>Adobe Real-time CDP necessita di autorizzazioni `write` sull&#39;oggetto bucket in cui verranno inviati i file di esportazione.
