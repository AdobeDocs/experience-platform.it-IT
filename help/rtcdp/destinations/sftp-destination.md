---
title: Destinazione SFTP
seo-title: Destinazione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
seo-description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
translation-type: tm+mt
source-git-commit: 098dd31be4d6ee6971cd87bcbfe0f686e34918e1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# Destinazione SFTP

## Panoramica

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.

Per esportare i dati, effettua i seguenti passaggi:

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso SFTP.

Per le destinazioni SFTP, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione, nel passaggio **Autenticazione** :

* **Host**: l&#39;indirizzo della posizione di archiviazione SFTP
* **Nome utente**: il nome utente per accedere al percorso di archiviazione SFTP
* **Password**: la password per accedere al percorso di archiviazione SFTP

## Dati esportati {#exported-data}

Per [!SFTP] le destinazioni,  Adobe CDP in tempo reale crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione specificato. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.