---
keywords: SFTP;sftp
title: Destinazione SFTP
seo-title: Destinazione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
seo-description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
translation-type: tm+mt
source-git-commit: 7484e64d0d359f40ef242dfc9d2d1704018a8ed6
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Destinazione SFTP

## Panoramica

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.

## Tipo esportazione {#export-type}

**Basato** su profilo: si esportano tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata degli attributi selezionati del flusso di lavoro [di attivazione della](../../ui/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Destinazione Connect {#connect-destination}

Consulta Flusso di lavoro delle destinazioni di archiviazione [Cloud ](./workflow.md)per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso SFTP.

Per le destinazioni SFTP, immetti le seguenti informazioni nel flusso di lavoro di creazione della destinazione, nel passaggio **Autenticazione** :

* **Host**: L&#39;indirizzo del percorso di archiviazione SFTP
* **Nome utente**: Il nome utente per accedere al percorso di archiviazione SFTP
* **Password**: La password per accedere al percorso di archiviazione SFTP

## Dati esportati {#exported-data}

Per le destinazioni SFTP, in tempo reale CDP crea un file delimitato da tabulazioni `.txt` o `.csv` nel percorso di memorizzazione fornito. Per ulteriori informazioni sui file, vedi Destinazioni di marketing [e-mail e destinazioni](../../ui/activate-destinations.md#esp-and-cloud-storage) di archiviazione cloud nell&#39;esercitazione sull&#39;attivazione del segmento.