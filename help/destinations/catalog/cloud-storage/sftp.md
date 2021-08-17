---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '281'
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

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **Host**: Indirizzo del percorso di archiviazione SFTP
* **Nome utente**: Nome utente per accedere al percorso di archiviazione SFTP
* **Password**: Password per accedere al percorso di archiviazione SFTP
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Percorso]** cartella: immetti il percorso della cartella di destinazione che ospiterà i file esportati.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

## Dati esportati {#exported-data}

Per le destinazioni [!DNL SFTP], Platform crea un file `.csv` delimitato da tabulazioni nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Destinazioni di e-mail marketing e destinazioni di archiviazione Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) nell’esercitazione sull’attivazione dei segmenti.

## ELENCO CONSENTITI di indirizzo IP

Per aggiungere IP di Adobe a un elenco consentiti, fai riferimento all’ [elenco consentiti di indirizzi IP per le destinazioni di archiviazione cloud](ip-address-allow-list.md) .
