---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Connessione SFTP

## Panoramica {#overview}

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Mentre Adobe supporta le esportazioni di dati verso server SFTP, le posizioni di archiviazione cloud consigliate per l’esportazione di dati sono [!DNL Amazon S3] e [!DNL Azure Blob].

## Tipo di esportazione {#export-type}

**Basato su profilo** : stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto dalla schermata seleziona attributi del flusso di lavoro [ di attivazione della ](../../ui/activate-destinations.md#select-attributes)destinazione.

![Tipo di esportazione basato su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Collegare la destinazione {#connect-destination}

Per istruzioni su come connettersi alle destinazioni di archiviazione cloud, incluso SFTP, fai riferimento al [flusso di lavoro delle destinazioni di archiviazione cloud ](./workflow.md) .

Per le destinazioni SFTP, inserisci le seguenti informazioni nel flusso di lavoro di creazione della destinazione, nel passaggio **Autenticazione** :

* **Host**: Indirizzo del percorso di archiviazione SFTP
* **Nome utente**: Nome utente per accedere al percorso di archiviazione SFTP
* **Password**: Password per accedere al percorso di archiviazione SFTP

## Dati esportati {#exported-data}

Per le destinazioni SFTP, Platform crea un file `.txt` o `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.

## ELENCO CONSENTITI di indirizzo IP

Per aggiungere IP di Adobe a un elenco consentiti, fai riferimento all’ [elenco consentiti di indirizzi IP per le destinazioni di archiviazione cloud](./ip-address-allow-list.md) .