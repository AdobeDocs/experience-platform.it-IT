---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da  Experience Platform.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Connessione SFTP

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