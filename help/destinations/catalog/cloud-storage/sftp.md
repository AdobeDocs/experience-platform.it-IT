---
title: Connessione SFTP
description: Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 8%

---

# Connessione SFTP

## Registro modifiche destinazione {#changelog}

Con la versione di Experience Platform di luglio 2023, la destinazione SFTP fornisce nuove funzionalità, come elencato di seguito:

* [Supporto per l’esportazione di set di dati](/help/destinations/ui/export-datasets.md).
* Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilità di personalizzare la formattazione dei file CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Panoramica {#overview}

Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Sebbene Experience Platform supporti le esportazioni di dati ai server SFTP, i percorsi consigliati per l&#39;archiviazione cloud per l&#39;esportazione dei dati sono [!DNL Amazon S3] e [!DNL Azure Blob].

## Connessione a SFTP tramite API o interfaccia utente {#connect-api-or-ui}

* Per connetterti al percorso di archiviazione SFTP utilizzando l&#39;interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva i tipi di pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione SFTP a livello di programmazione, leggi [Attiva i tipi di pubblico in destinazioni basate su file tramite l&#39;esercitazione API del servizio Flusso](../../api/activate-segments-file-based-destinations.md).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Tipo di esportazione basato su profilo SFTP evidenziato nel catalogo delle destinazioni.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Esporta set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Come [esportare i set di dati utilizzando l&#39;interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Come [esportare i set di dati a livello di programmazione utilizzando l&#39;API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l&#39;esportazione di *dati sul pubblico*, Platform crea un file `.csv`, `parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [formati di file supportati per l&#39;esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell&#39;esercitazione di Audience Activation.

Durante l&#39;esportazione di *set di dati*, Platform crea un file `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [Verifica dell&#39;esportazione dei set di dati](../../ui/export-datasets.md#verify) nell&#39;esercitazione sull&#39;esportazione dei set di dati.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chiave SSH privata"
>abstract="La chiave SSH privata deve essere una stringa in formato RSA con codifica Base64 e non deve essere protetta da password."

Se selezioni il tipo di autenticazione **[!UICONTROL SFTP con password]** per connettersi alla posizione SFTP:

![Autenticazione di base della destinazione SFTP con password.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Dominio]**: indirizzo del percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: il nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Porta]**: la porta utilizzata dal percorso di archiviazione SFTP;
* **[!UICONTROL Password]**: password per accedere al percorso di archiviazione SFTP.
* **[!UICONTROL Chiave di crittografia]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell&#39;interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se selezioni il tipo di autenticazione **[!UICONTROL SFTP con chiave SSH]** per connettersi alla posizione SFTP:

![Autenticazione della chiave SSH di destinazione SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: inserisci l&#39;indirizzo IP o il nome di dominio del tuo account SFTP
* **[!UICONTROL Porta]**: la porta utilizzata dal percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: il nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Chiave SSH]**: chiave SSH privata utilizzata per accedere al percorso di archiviazione SFTP. La chiave privata deve essere una stringa in formato RSA con codifica Base64 e non deve essere protetta da password.
* **[!UICONTROL Chiave di crittografia]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell&#39;interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione alla posizione SFTP, fornisci le seguenti informazioni per la destinazione:

![Campi dei dettagli della destinazione per la destinazione SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: immetti un nome che ti consenta di identificare questa destinazione nell&#39;interfaccia utente di Experience Platform;
* **[!UICONTROL Descrizione]**: immettere una descrizione per questa destinazione;
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella nel percorso SFTP in cui verranno esportati i file.
* **[!UICONTROL Tipo di file]**: selezionare il formato da utilizzare per i file esportati dall&#39;Experience Platform. Quando selezioni l&#39;opzione [!UICONTROL CSV], puoi anche [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: selezionare il tipo di compressione che Experience Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attivare questa opzione se si desidera che le esportazioni includano un file JSON manifesto contenente informazioni sul percorso di esportazione, sulle dimensioni dell&#39;esportazione e altro ancora. Il manifesto è denominato nel formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: il percorso nel percorso di archiviazione in cui è depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla l’archiviazione SFTP e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allow-list}

Se hai bisogno di aggiungere IP di Adobe inserii nell&#39;elenco Consentiti a un inserisco nell&#39;elenco Consentiti di, consulta l&#39;articolo [Indirizzo IP ](ip-address-allow-list.md).
