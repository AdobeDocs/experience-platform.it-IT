---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# Connessione SFTP

## Panoramica {#overview}

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Sebbene Adobe supporti le esportazioni di dati verso server SFTP, le posizioni di archiviazione cloud consigliate per esportare i dati sono [!DNL Amazon S3] e [!DNL Azure Blob].

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo di esportazione basato su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata Base64."
>text="Learn more in documentation"

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **Host**: Indirizzo del percorso di archiviazione SFTP
* **Nome utente**: Nome utente per accedere al percorso di archiviazione SFTP
* **Password**: Password per accedere al percorso di archiviazione SFTP
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.

## Dati esportati {#exported-data}

Per [!DNL SFTP] destinazioni, Platform crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) nell’esercitazione sull’attivazione dei segmenti.

## ELENCO CONSENTITI di indirizzo IP

Fai riferimento a [ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud](ip-address-allow-list.md) se devi aggiungere IP di Adobe a un elenco consentiti.
