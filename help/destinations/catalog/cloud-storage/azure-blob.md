---
title: Connessione BLOB di Azure
description: Crea una connessione in uscita all’archiviazione BLOB di Azure per esportare periodicamente i file di dati CSV da Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 7%

---

# Connessione [!DNL Azure Blob]

## Registro modifiche destinazione {#changelog}

Con la versione di Experience Platform di luglio 2023, la destinazione [!DNL Azure Blob] fornisce nuove funzionalità, come elencato di seguito:

* [Supporto per l’esportazione di set di dati](/help/destinations/ui/export-datasets.md).
* Nuove [opzioni di denominazione file](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Possibilità di impostare intestazioni di file personalizzate nei file esportati tramite il [passaggio di mappatura migliorato](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Possibilità di personalizzare la formattazione dei file CSV esportati](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Panoramica {#overview}

[!DNL Azure Blob] (di seguito [!DNL Blob]) è la soluzione di archiviazione oggetti di Microsoft per il cloud. Questo tutorial descrive i passaggi per creare una destinazione [!DNL Blob] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Connettersi all&#39;archiviazione [!UICONTROL BLOB di Azure] tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al percorso di archiviazione [!UICONTROL BLOB di Azure] tramite l&#39;interfaccia utente di Platform, leggere le sezioni [Connetti alla destinazione](#connect) e [Attiva i tipi di pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione [!UICONTROL BLOB di Azure] a livello di programmazione, leggere l&#39;esercitazione [Attiva tipi di pubblico in destinazioni basate su file](../../api/activate-segments-file-based-destinations.md).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una destinazione [!DNL Blob] valida, puoi saltare il resto del documento e passare all&#39;esercitazione sull&#39;[attivazione dei tipi di pubblico nella tua destinazione](../../ui/activate-batch-profile-destinations.md).

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

### Autenticarsi nella destinazione {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi collegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Nel collegamento alla documentazione qui di seguito, trovi un esempio di chiave formattata correttamente."

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Stringa di connessione]**: la stringa di connessione è necessaria per accedere ai dati nell&#39;archiviazione BLOB. Il modello di stringa di connessione [!DNL Blob] inizia con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Per ulteriori informazioni sulla configurazione della stringa di connessione [!DNL Blob], vedere [Configurare una stringa di connessione per un account di archiviazione Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) nella documentazione di Microsoft.
* **[!UICONTROL Chiave di crittografia]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell&#39;interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere un nome che consenta di identificare la destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Percorso cartella]**: immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Contenitore]**: immettere il nome del contenitore [!DNL Azure Blob Storage] da utilizzare per questa destinazione.
* **[!UICONTROL Tipo di file]**: selezionare il formato da utilizzare per i file esportati dall&#39;Experience Platform. Quando selezioni l&#39;opzione [!UICONTROL CSV], puoi anche [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: selezionare il tipo di compressione che Experience Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attivare questa opzione se si desidera che le esportazioni includano un file JSON manifesto contenente informazioni sul percorso di esportazione, sulle dimensioni dell&#39;esportazione e altro ancora. Il manifesto è denominato nel formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: il percorso nel percorso di archiviazione in cui è depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controllare l&#39;archivio [!DNL Azure Blob] e assicurarsi che i file esportati contengano le popolazioni di profilo previste.