---
keywords: SFTP;sftp
title: Connessione SFTP
description: Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 8%

---

# Connessione SFTP

## Registro modifiche destinazione {#changelog}

>[!IMPORTANT]
>
>Con la versione beta della funzionalità di esportazione dei set di dati e la migliorata funzionalità di esportazione dei file, ora potresti vedere due [!DNL SFTP] nel catalogo delle destinazioni.
>* Se si stanno già esportando file in **[!UICONTROL SFTP]** destinazione: crea nuovi flussi di dati per il nuovo **[!UICONTROL SFTP beta]** destinazione.
>* Se non hai ancora creato flussi di dati per **[!UICONTROL SFTP]** destinazione, utilizza il nuovo **[!UICONTROL SFTP beta]** scheda in cui esportare i file **[!UICONTROL SFTP]**.


![Immagine delle due schede di destinazione SFTP in una visualizzazione affiancata.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Miglioramenti nel nuovo [!DNL SFTP] la scheda di destinazione include:

* [Supporto per l’esportazione del set di dati](/help/destinations/ui/export-datasets.md).
* Aggiuntivo [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Panoramica {#overview}

Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Sebbene Experience Platform supporti le esportazioni di dati ai server SFTP, le posizioni di archiviazione cloud consigliate per l’esportazione dei dati sono [!DNL Amazon S3] e [!DNL SFTP].

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo di esportazione basata su profilo SFTP](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chiave SSH privata"
>abstract="La chiave SSH privata deve essere formattata come stringa con codifica Base64 e non deve essere protetta da password."

Se si seleziona la **[!UICONTROL Autenticazione di base]** digita per connetterti alla posizione SFTP:

![Autenticazione di base della destinazione SFTP](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: indirizzo del percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Password]**: password per accedere al percorso di archiviazione SFTP.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se si seleziona la **[!UICONTROL SFTP con chiave SSH]** tipo di autenticazione per connettersi alla posizione SFTP:

![Autenticazione della chiave SSH di destinazione SFTP](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: inserisci l’indirizzo IP o il nome di dominio dell’account SFTP
* **[!UICONTROL Porta]**: porta utilizzata dalla posizione di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Chiave SSH]**: chiave SSH privata utilizzata per accedere al percorso di archiviazione SFTP. La chiave privata deve essere formattata come stringa con codifica Base64 e non deve essere protetta da password.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

   ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione alla posizione SFTP, fornisci le seguenti informazioni per la destinazione:

![Dettagli di destinazione disponibili per la destinazione SFTP](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: inserisci un nome che ti aiuterà a identificare questa destinazione nell’interfaccia utente di Experience Platform;
* **[!UICONTROL Descrizione]**: inserire una descrizione per questa destinazione;
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella nel percorso SFTP in cui verranno esportati i file.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Questa opzione è disponibile solo per **[!UICONTROL SFTP beta]** destinazione. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experience Platform deve utilizzare per i file esportati. Questa opzione è disponibile solo per **[!UICONTROL SFTP beta]** destinazione.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, leggi [tutorial sull’esportazione dei set di dati](/help/destinations/ui/export-datasets.md).

## Dati esportati {#exported-data}

Per [!DNL SFTP] destinazioni, Platform crea un’ `.csv` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) nell’esercitazione di attivazione dei segmenti.

## ELENCO CONSENTITI di indirizzo IP

Fai riferimento a [ELENCO CONSENTITI di indirizzo IP per le destinazioni di archiviazione cloud](ip-address-allow-list.md) se devi aggiungere IP di Adobe a un elenco consentiti.
