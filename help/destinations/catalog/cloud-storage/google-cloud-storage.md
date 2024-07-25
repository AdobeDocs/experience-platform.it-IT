---
title: Connessione Google Cloud Storage
description: Scopri come connettersi a Google Cloud Storage e attivare tipi di pubblico o esportare set di dati.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: f652faac7d771b590b30f591616b53d0cd2ff1eb
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 2%

---

# Connessione [!DNL Google Cloud Storage]

## Panoramica {#overview}

Crea una connessione in uscita a [!DNL Google Cloud Storage] per esportare periodicamente i file di dati da Adobe Experience Platform nei bucket.

## Connettersi all&#39;archiviazione [!DNL Google Cloud Storage] tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al percorso di archiviazione [!DNL Google Cloud Storage] tramite l&#39;interfaccia utente di Platform, leggere le sezioni [Connetti alla destinazione](#connect) e [Attiva i tipi di pubblico a questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione [!DNL Google Cloud Storage] a livello di programmazione, leggere l&#39;esercitazione [Attiva tipi di pubblico in destinazioni basate su file](../../api/activate-segments-file-based-destinations.md).

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
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili, come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Esporta set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Come [esportare i set di dati utilizzando l&#39;interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Come [esportare i set di dati a livello di programmazione utilizzando l&#39;API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l&#39;esportazione di *dati sul pubblico*, Platform crea un file `.csv`, `parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [formati di file supportati per l&#39;esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell&#39;esercitazione di Audience Activation.

Durante l&#39;esportazione di *set di dati*, Platform crea un file `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [Verifica dell&#39;esportazione dei set di dati](../../ui/export-datasets.md#verify) nell&#39;esercitazione sull&#39;esportazione dei set di dati.

## Configurazione dei prerequisiti per la connessione all&#39;account [!DNL Google Cloud Storage] {#prerequisites}

Per connettere Platform a [!DNL Google Cloud Storage], devi prima abilitare l&#39;interoperabilità per il tuo account [!DNL Google Cloud Storage]. Per accedere all&#39;impostazione di interoperabilità, apri [!DNL Google Cloud Platform] e seleziona **[!UICONTROL Impostazioni]** dall&#39;opzione **[!UICONTROL Archiviazione cloud]** nel pannello di navigazione.

![Dashboard di Google Cloud Platform con archiviazione cloud e impostazioni evidenziate.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

Viene visualizzata la pagina **[!UICONTROL Impostazioni]**. Da qui puoi visualizzare informazioni relative al tuo ID progetto [!DNL Google] e dettagli sul tuo account [!DNL Google Cloud Storage]. Per accedere alle impostazioni di interoperabilità, seleziona **[!UICONTROL Interoperabilità]** dall&#39;intestazione superiore.

![Scheda Interoperabilità evidenziata nel dashboard di Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

La pagina **[!UICONTROL Interoperabilità]** contiene informazioni sull&#39;autenticazione, le chiavi di accesso e il progetto predefinito associato all&#39;account del servizio. Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per l&#39;account del servizio, selezionare **[!UICONTROL Crea una chiave per un account del servizio]**.

![Creare una chiave per un controllo account di servizio evidenziato nel dashboard di Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puoi utilizzare l&#39;ID della chiave di accesso e la chiave di accesso segreta appena generati per collegare l&#39;account [!DNL Google Cloud Storage] a Platform.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](/help/destinations/ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: una stringa alfanumerica di 61 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. Per informazioni su come ottenere questo valore, leggi la sezione [prerequisiti](#prerequisites) precedente.
* **[!UICONTROL Chiave di accesso segreta]**: una stringa con codifica base64 di 40 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. Per informazioni su come ottenere questo valore, leggi la sezione [prerequisiti](#prerequisites) precedente.
* **[!UICONTROL Chiave di crittografia]**: facoltativamente, è possibile allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell&#39;interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Per ulteriori informazioni su questi valori, leggere la guida delle [chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica sull&#39;origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Nome bucket]**: immettere il nome del bucket [!DNL Google Cloud Storage] da utilizzare per questa destinazione.
* **[!UICONTROL Percorso cartella]**: immettere il percorso della cartella di destinazione che ospiterà i file esportati.
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

### Autorizzazioni [!DNL Google Cloud Storage] richieste {#required-google-cloud-storage-permission}

Per connettersi ed esportare correttamente i dati nel percorso di archiviazione [!DNL Google Cloud Storage], sono necessarie le seguenti autorizzazioni [!DNL Google Cloud Storage] per i bucket:

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

Ulteriori informazioni su [controllo degli accessi e autorizzazioni](https://cloud.google.com/storage/docs/access-control/iam-permissions) in [!DNL Google Cloud Storage].

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

### Pianificazione

Nel passaggio **[!UICONTROL Pianificazione]**, puoi [impostare la pianificazione dell&#39;esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per la destinazione [!DNL Google Cloud Storage] e [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

Nel passaggio **[!UICONTROL Mappatura]**, puoi selezionare l&#39;attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedi il [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell&#39;esercitazione dell&#39;interfaccia utente per l&#39;attivazione di destinazioni batch.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla il bucket [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allow-list}

Se hai bisogno di aggiungere IP di Adobe inserii nell&#39;elenco Consentiti a un inserisco nell&#39;elenco Consentiti di, consulta l&#39;articolo [Indirizzo IP ](ip-address-allow-list.md).