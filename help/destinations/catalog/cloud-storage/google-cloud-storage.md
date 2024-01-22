---
title: Connessione Google Cloud Storage
description: Scopri come connettersi a Google Cloud Storage e attivare tipi di pubblico o esportare set di dati.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] connessione

## Panoramica {#overview}

Creare una connessione in uscita a [!DNL Google Cloud Storage] per esportare periodicamente file di dati da Adobe Experience Platform nei bucket personali.

## Connetti al tuo [!DNL Google Cloud Storage] archiviazione tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al tuo [!DNL Google Cloud Storage] percorso di archiviazione tramite l’interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva il pubblico in questa destinazione](#activate) di seguito.
* Per connettersi al tuo [!DNL Google Cloud Storage] percorso di archiviazione a livello di programmazione, leggere [Attiva i tipi di pubblico in destinazioni basate su file utilizzando l’esercitazione API del servizio Flusso](../../api/activate-segments-file-based-destinations.md).

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
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili, come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Configurazione dei prerequisiti per la connessione [!DNL Google Cloud Storage] account {#prerequisites}

Per collegare Platform a [!DNL Google Cloud Storage], è necessario innanzitutto abilitare l&#39;interoperabilità per [!DNL Google Cloud Storage] account. Per accedere all&#39;impostazione di interoperabilità, aprire [!DNL Google Cloud Platform] e seleziona **[!UICONTROL Impostazioni]** dal **[!UICONTROL Archiviazione cloud]** nel pannello di navigazione.

![Dashboard della piattaforma Google Cloud con archiviazione e impostazioni cloud evidenziate.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

Il **[!UICONTROL Impostazioni]** viene visualizzata. Da qui puoi vedere le informazioni relative al tuo [!DNL Google] ID progetto e dettagli sul tuo [!DNL Google Cloud Storage] account. Per accedere alle impostazioni di interoperabilità, seleziona **[!UICONTROL Interoperabilità]** dall’intestazione in alto.

![La scheda Interoperabilità è evidenziata nel dashboard della piattaforma Google Cloud.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

Il **[!UICONTROL Interoperabilità]** La pagina contiene informazioni sull’autenticazione, le chiavi di accesso e il progetto predefinito associato al tuo account di servizio. Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per il tuo account di servizio, seleziona **[!UICONTROL Creare una chiave per un account di servizio]**.

![La sezione Creare una chiave per un controllo account di servizio è evidenziata nel dashboard di Google Cloud Platform.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Puoi utilizzare l’ID della chiave di accesso e la chiave di accesso segreta appena generati per collegare il tuo [!DNL Google Cloud Storage] da un account a Platform.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](/help/destinations/ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL ID chiave di accesso]**: stringa alfanumerica di 61 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. Per informazioni su come ottenere questo valore, leggi [prerequisiti](#prerequisites) sopra.
* **[!UICONTROL Chiave di accesso segreta]**: stringa con codifica base64 di 40 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. Per informazioni su come ottenere questo valore, leggi [prerequisiti](#prerequisites) sopra.
* **[!UICONTROL Chiave di crittografia]**: in alternativa, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. Visualizza un esempio di chiave di crittografia formattata correttamente nell’immagine seguente.

  ![Immagine che mostra un esempio di chiave PGP formattata correttamente nell’interfaccia utente](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Per ulteriori informazioni su questi valori, leggere [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica dell’origine](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Nome bucket]**: immetti il nome del [!DNL Google Cloud Storage] bucket da utilizzare per questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experienci Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attiva questa opzione se desideri che le esportazioni includano un file JSON manifesto contenente informazioni sulla posizione di esportazione, sulle dimensioni di esportazione e altro ancora. Il manifesto viene denominato utilizzando il formato `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visualizza un [file manifesto di esempio](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Il file manifesto include i campi seguenti:
   * `flowRunId`: Il [esecuzione del flusso di dati](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) che ha generato il file esportato.
   * `scheduledTime`: ora in UTC in cui è stato esportato il file.
   * `exportResults.sinkPath`: percorso nel percorso di archiviazione in cui viene depositato il file esportato.
   * `exportResults.name`: nome del file esportato.
   * `size`: dimensione del file esportato, in byte.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Pianificazione

In **[!UICONTROL Pianificazione]** passaggio, puoi [impostare la pianificazione di esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per [!DNL Google Cloud Storage] e puoi anche [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** fase, puoi selezionare l’attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedere [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione dell’interfaccia utente attiva destinazioni batch.

## Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Procedura [esportare i set di dati utilizzando l’interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Procedura [esportare i set di dati a livello di programmazione utilizzando l’API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla [!DNL Google Cloud Storage] e assicurati che i file esportati contengano le popolazioni di profilo previste.
