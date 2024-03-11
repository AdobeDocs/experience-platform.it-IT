---
title: Connessione SFTP
description: Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
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
* [Possibilità di personalizzare la formattazione dei file di dati CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Panoramica {#overview}

Crea una connessione in uscita al server SFTP per esportare periodicamente file di dati delimitati da Adobe Experience Platform.

>[!IMPORTANT]
>
> Sebbene Experienci Platform supporti le esportazioni di dati ai server SFTP, le posizioni di archiviazione cloud consigliate per l’esportazione dei dati sono [!DNL Amazon S3] e [!DNL Azure Blob].

## Connessione a SFTP tramite API o interfaccia utente {#connect-api-or-ui}

* Per connetterti al percorso di archiviazione SFTP utilizzando l’interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva il pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione SFTP a livello di programmazione, leggi la [Attiva i tipi di pubblico in destinazioni basate su file utilizzando l’esercitazione API del servizio Flusso](../../api/activate-segments-file-based-destinations.md).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Il tipo di esportazione basato su profilo SFTP è evidenziato nel catalogo delle destinazioni.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Procedura [esportare i set di dati utilizzando l’interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Procedura [esportare i set di dati a livello di programmazione utilizzando l’API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l’esportazione *dati sul pubblico*, Platform crea un `.csv`, `parquet`, o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedere [formati di file supportati per l’esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell’esercitazione di Audience Activation.

Durante l’esportazione *set di dati*, Platform crea un `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, vedere [verificare la corretta esportazione del set di dati](../../ui/export-datasets.md#verify) nell’esercitazione esportare set di dati.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Informazioni di autenticazione {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Chiave SSH privata"
>abstract="La chiave SSH privata deve essere una stringa in formato RSA con codifica Base64 e non deve essere protetta da password."

Se si seleziona la **[!UICONTROL SFTP con password]** tipo di autenticazione per connettersi alla posizione SFTP:

![Autenticazione di base della destinazione SFTP con password.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Dominio]**: indirizzo del percorso di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Porta]**: porta utilizzata dalla posizione di archiviazione SFTP;
* **[!UICONTROL Password]**: password per accedere al percorso di archiviazione SFTP.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Se si seleziona la **[!UICONTROL SFTP con chiave SSH]** tipo di autenticazione per connettersi alla posizione SFTP:

![Autenticazione della chiave SSH di destinazione SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Dominio]**: inserisci l’indirizzo IP o il nome di dominio dell’account SFTP
* **[!UICONTROL Porta]**: porta utilizzata dalla posizione di archiviazione SFTP;
* **[!UICONTROL Nome utente]**: nome utente per accedere al percorso di archiviazione SFTP;
* **[!UICONTROL Chiave SSH]**: chiave SSH privata utilizzata per accedere al percorso di archiviazione SFTP. La chiave privata deve essere una stringa in formato RSA con codifica Base64 e non deve essere protetta da password.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione alla posizione SFTP, fornisci le seguenti informazioni per la destinazione:

![Campi dei dettagli della destinazione SFTP.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Nome]**: immetti un nome che ti aiuti a identificare questa destinazione nell’interfaccia utente di Experienci Platform;
* **[!UICONTROL Descrizione]**: inserire una descrizione per questa destinazione;
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella nel percorso SFTP in cui verranno esportati i file.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experienci Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attiva questa opzione se desideri che le esportazioni includano un file JSON manifesto contenente informazioni sulla posizione di esportazione, sulle dimensioni di esportazione e altro ancora. Il manifesto viene denominato utilizzando il formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: Il [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: percorso nel percorso di archiviazione in cui viene depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla l’archiviazione SFTP e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Indirizzo IP inserito nell&#39;elenco Consentiti {#ip-address-allow-list}

Consulta la sezione [Indirizzo IP inserito nell&#39;elenco Consentiti](ip-address-allow-list.md) articolo per aggiungere IP di Adobe a un inserisco nell&#39;elenco Consentiti di.
