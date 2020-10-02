---
keywords: SFTP;sftp
title: Destinazione SFTP
seo-title: Destinazione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
seo-description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
translation-type: tm+mt
source-git-commit: d0a04c61bfe4024a2bb45ea7babab9073fcd6c22
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Destinazione SFTP

## Panoramica

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.

## Tipo esportazione {#export-type}

**Esportazione** profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [di attivazione della](/help/rtcdp/destinations/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo SFTP](/help/rtcdp/destinations/assets/sftp-export-type.png)

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso SFTP.

Per le destinazioni SFTP, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione, nel passaggio **Autenticazione** :

* **Host**: l&#39;indirizzo della posizione di archiviazione SFTP
* **Nome utente**: il nome utente per accedere al percorso di archiviazione SFTP
* **Password**: la password per accedere al percorso di archiviazione SFTP

## Dati esportati {#exported-data}

Per le destinazioni SFTP,  CDP in tempo reale Adobe crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione fornito dall&#39;utente. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.