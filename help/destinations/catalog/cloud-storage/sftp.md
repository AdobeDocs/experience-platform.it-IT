---
keywords: SFTP;sftp
title: Destinazione SFTP
seo-title: Destinazione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
seo-description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Destinazione SFTP

## Panoramica

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.

## Tipo di esportazione {#export-type}

**Basato**  su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Destinazione Connect {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso SFTP, vedere [Flusso di lavoro delle destinazioni di archiviazione cloud ](./workflow.md).

Per le destinazioni SFTP, immettete le seguenti informazioni nel flusso di lavoro di creazione della destinazione, nel passaggio **Authentication**:

* **Host**: L&#39;indirizzo del percorso di archiviazione SFTP
* **Nome utente**: Il nome utente per accedere al percorso di archiviazione SFTP
* **Password**: La password per accedere al percorso di archiviazione SFTP

## Dati esportati {#exported-data}

Per le destinazioni SFTP, Platform crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione fornito dall&#39;utente. Per ulteriori informazioni sui file, vedi [Destinazioni di marketing e archiviazione di e-mail e Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell&#39;esercitazione sull&#39;attivazione dei segmenti.