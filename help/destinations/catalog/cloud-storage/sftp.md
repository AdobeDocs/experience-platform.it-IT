---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Connessione SFTP

## Passaggio alla destinazione {#changelog}

>[!IMPORTANT]
>
>Con la versione beta della funzionalità dei set di dati per l’esportazione e la funzionalità di esportazione dei file migliorata, ora potrebbero essere disponibili due [!DNL SFTP] nel catalogo delle destinazioni.
>* Se si esportano già i file in **[!UICONTROL SFTP]** destinazione: Crea nuovi flussi di dati per il nuovo **[!UICONTROL Beta SFTP]** destinazione.
>* Se non hai ancora creato alcun flusso di dati per il **[!UICONTROL SFTP]** destinazione, utilizzare il nuovo **[!UICONTROL Beta SFTP]** scheda per esportare i file in **[!UICONTROL SFTP]**.


![Immagine delle due schede di destinazione SFTP affiancata.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Miglioramenti nel nuovo [!DNL SFTP] la scheda di destinazione include:

* [Supporto per l&#39;esportazione di set di dati](/help/destinations/ui/export-datasets.md).
* Aggiuntivo [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Panoramica {#overview}

Crea una connessione in uscita dal vivo al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Sebbene Experience Platform supporti le esportazioni di dati verso server SFTP, le posizioni di archiviazione cloud consigliate per esportare i dati sono [!DNL Amazon S3] e [!DNL SFTP].

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

![Tipo di esportazione basato su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave formattata correttamente nel collegamento alla documentazione seguente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chiave SSH privata"
>abstract="La chiave SSH privata deve essere formattata come stringa codificata Base64 e non deve essere protetta da password."

Se selezioni la **[!UICONTROL Autenticazione di base]** digita per connetterti al tuo percorso SFTP:

![Autenticazione di base della destinazione SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: L&#39;indirizzo del percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: Nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Password]**: Password per accedere al percorso di archiviazione SFTP.
* **[!UICONTROL Chiave di crittografia]**: Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se selezioni la **[!UICONTROL SFTP con chiave SSH]** tipo di autenticazione per la connessione al percorso SFTP:

![Autenticazione chiave SSH di destinazione SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: Inserisci l’indirizzo IP o il nome di dominio del tuo account SFTP
* **[!UICONTROL Porta]**: La porta utilizzata dal percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: Nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Chiave SSH]**: Chiave SSH privata utilizzata per accedere al percorso di archiviazione SFTP. La chiave privata deve essere formattata come stringa codificata Base64 e non deve essere protetta da password.
* **[!UICONTROL Chiave di crittografia]**: Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione per la posizione SFTP, fornisci le seguenti informazioni per la destinazione:

![Dettagli di destinazione disponibili per la destinazione SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione nell’interfaccia utente di Experience Platform;
* **[!UICONTROL Descrizione]**: inserire una descrizione della destinazione;
* **[!UICONTROL Percorso cartella]**: inserisci il percorso della cartella nel percorso SFTP in cui verranno esportati i file.
* **[!UICONTROL Tipo di file]**: selezionare l&#39;Experience Platform di formato da utilizzare per i file esportati. Questa opzione è disponibile solo per **[!UICONTROL Beta SFTP]** destinazione. Quando selezioni [!UICONTROL CSV] è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: selezionare il tipo di compressione che l&#39;Experience Platform deve utilizzare per i file esportati. Questa opzione è disponibile solo per **[!UICONTROL Beta SFTP]** destinazione.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta la sezione [esercitazione sui set di dati di esportazione](/help/destinations/ui/export-datasets.md).

## Dati esportati {#exported-data}

Per [!DNL SFTP] destinazioni, Platform crea un `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) nell’esercitazione sull’attivazione dei segmenti.

## ELENCO CONSENTITI di indirizzo IP

Fai riferimento a [ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud](ip-address-allow-list.md) se devi aggiungere IP di Adobe a un elenco consentiti.
