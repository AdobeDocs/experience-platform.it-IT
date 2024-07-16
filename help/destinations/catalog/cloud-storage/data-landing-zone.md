---
title: Destinazione Data Landing Zone
description: Scopri come connettersi alla Data Landing Zone per attivare tipi di pubblico ed esportare set di dati.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: ce78e320e78a67cd744fdf1c49b34f6fcddf4f15
workflow-type: tm+mt
source-wordcount: '1592'
ht-degree: 4%

---

# Destinazione Data Landing Zone

>[!IMPORTANT]
>
>Questa pagina della documentazione fa riferimento alla [!DNL Data Landing Zone] *destinazione*. Esiste anche un [!DNL Data Landing Zone] *source* nel catalogo delle origini. Per ulteriori informazioni, leggere la documentazione di [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md).


## Panoramica {#overview}

[!DNL Data Landing Zone] è un’interfaccia di archiviazione [!DNL Azure Blob] fornita da Adobe Experience Platform che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per esportare i file da Platform. È possibile accedere a un contenitore [!DNL Data Landing Zone] per sandbox e il volume totale di dati in tutti i contenitori è limitato ai dati totali forniti con la licenza di Platform Products and Services. Per tutti i clienti di Platform e delle relative applicazioni, ad esempio [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] e [!DNL Real-Time Customer Data Platform], viene eseguito il provisioning con un contenitore [!DNL Data Landing Zone] per sandbox. È possibile leggere e scrivere file nel contenitore tramite [!DNL Azure Storage Explorer] o l&#39;interfaccia della riga di comando.

[!DNL Data Landing Zone] supporta l&#39;autenticazione basata su SAS e i relativi dati sono protetti con meccanismi di protezione di archiviazione standard [!DNL Azure Blob] in modalità di riposo e transito. SAS sta per [firma di accesso condiviso](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

L&#39;autenticazione basata su SAS consente di accedere in modo sicuro al contenitore [!DNL Data Landing Zone] tramite una connessione Internet pubblica. Non sono necessarie modifiche di rete per accedere al contenitore [!DNL Data Landing Zone], pertanto non è necessario configurare elenchi consentiti o impostazioni per più aree geografiche per la rete.

Platform applica un TTL (time-to-live) di sette giorni rigoroso su tutti i file caricati in un contenitore [!DNL Data Landing Zone]. Tutti i file vengono eliminati dopo sette giorni.

## Connettiti all&#39;archivio [!UICONTROL Data Landing Zone] tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al percorso di archiviazione [!UICONTROL Data Landing Zone] tramite l&#39;interfaccia utente di Platform, leggere le sezioni [Connetti alla destinazione](#connect) e [Attiva i tipi di pubblico a questa destinazione](#activate) di seguito.
* Per connettersi al percorso di archiviazione [!UICONTROL Data Landing Zone] a livello di programmazione, leggere l&#39;esercitazione [Attiva tipi di pubblico in destinazioni basate su file](../../api/activate-segments-file-based-destinations.md).

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
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata Seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Esporta set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Come [esportare i set di dati utilizzando l&#39;interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Come [esportare i set di dati a livello di programmazione utilizzando l&#39;API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Formato file dei dati esportati {#file-format}

Durante l&#39;esportazione di *dati sul pubblico*, Platform crea un file `.csv`, `parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [formati di file supportati per l&#39;esportazione](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) nell&#39;esercitazione di Audience Activation.

Durante l&#39;esportazione di *set di dati*, Platform crea un file `.parquet` o `.json` nel percorso di archiviazione fornito. Per ulteriori informazioni sui file, consulta la sezione [Verifica dell&#39;esportazione dei set di dati](../../ui/export-datasets.md#verify) nell&#39;esercitazione sull&#39;esportazione dei set di dati.

## Prerequisiti {#prerequisites}

Prendere nota dei seguenti prerequisiti che devono essere soddisfatti prima di poter utilizzare la destinazione [!DNL Data Landing Zone].

### Connetti il contenitore [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer]

È possibile utilizzare [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) per gestire il contenuto del contenitore [!DNL Data Landing Zone]. Per iniziare a utilizzare [!DNL Data Landing Zone], devi prima recuperare le credenziali, inserirle in [!DNL Azure Storage Explorer] e connettere il contenitore [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer].

Nell&#39;interfaccia utente di [!DNL Azure Storage Explorer], selezionare l&#39;icona di connessione nella barra di navigazione a sinistra. Viene visualizzata la finestra **Seleziona risorsa** che fornisce le opzioni per la connessione. Selezionare **[!DNL Blob container]** per connettersi all&#39;archivio [!DNL Data Landing Zone].

![Selezionare la risorsa evidenziata nell&#39;interfaccia utente di Azure.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Selezionare **URL firma di accesso condiviso (SAS)** come metodo di connessione, quindi selezionare **Avanti**.

![Selezionare il metodo di connessione evidenziato nell&#39;interfaccia utente di Azure.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Dopo aver selezionato il metodo di connessione, è necessario fornire **nome visualizzato** e l&#39;URL SAS del contenitore **[!DNL Blob]** che corrisponde al contenitore [!DNL Data Landing Zone].

>[!BEGINSHADEBOX]

### Recupera le credenziali per [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Per recuperare le credenziali di [!DNL Data Landing Zone], è necessario utilizzare le API di Platform. La chiamata API per recuperare le credenziali è descritta di seguito. Per informazioni su come ottenere i valori richiesti per le intestazioni, consulta la [Guida introduttiva alle API di Adobe Experience Platform](/help/landing/api-guide.md).

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parametri della query | Descrizione |
| --- | --- |
| `dlz_destination` | Il tipo `dlz_destination` consente all&#39;API di distinguere un contenitore di destinazione di una zona di destinazione dagli altri tipi di contenitori disponibili. |

{style="table-layout:auto"}

**Richiesta**

L’esempio di richiesta seguente recupera le credenziali per una zona di destinazione esistente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La seguente risposta restituisce le informazioni sulle credenziali per la tua zona di destinazione, inclusi `SASToken` e `SASUri` correnti e `storageAccountName` che corrispondono al contenitore della tua zona di destinazione.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Proprietà | Descrizione |
| --- | --- |
| `containerName` | Il nome della zona di destinazione. |
| `SASToken` | Il token di firma di accesso condiviso per la tua zona di destinazione. Questa stringa contiene tutte le informazioni necessarie per autorizzare una richiesta. |
| `SASUri` | URI della firma di accesso condiviso per la zona di destinazione. Questa stringa è una combinazione dell&#39;URI della zona di destinazione per la quale si sta effettuando l&#39;autenticazione e del token SAS corrispondente, |

{style="table-layout:auto"}

### Aggiorna credenziali [!DNL Data Landing Zone] {#update-dlz-credentials}

Se necessario, puoi anche aggiornare le credenziali. È possibile aggiornare `SASToken` effettuando una richiesta POST all&#39;endpoint `/credentials` dell&#39;API [!DNL Connectors].

**Formato API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parametri della query | Descrizione |
| --- | --- |
| `dlz_destination` | Il tipo `dlz_destination` consente all&#39;API di distinguere un contenitore di destinazione di una zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | L&#39;azione `refresh` consente di reimpostare le credenziali della zona di destinazione e generare automaticamente un nuovo `SASToken`. |

{style="table-layout:auto"}

**Richiesta**

La richiesta seguente aggiorna le credenziali della zona di destinazione.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Risposta**

La seguente risposta restituisce valori aggiornati per `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Fornisci il nome visualizzato (`containerName`) e l&#39;URL SAS [!DNL Data Landing Zone], come restituito nella chiamata API descritta in precedenza, quindi seleziona **Avanti**.

![Immettere le informazioni di connessione evidenziate nell&#39;interfaccia utente di Azure.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Viene visualizzata la finestra **Riepilogo** che fornisce una panoramica delle impostazioni, incluse informazioni sull&#39;endpoint [!DNL Blob] e sulle autorizzazioni. Al termine, selezionare **Connetti**.

![Riepilogo delle impostazioni visualizzate nell&#39;interfaccia utente di Azure.](/help/sources/images/tutorials/create/dlz/summary.png)

Una connessione riuscita aggiorna l&#39;interfaccia utente di [!DNL Azure Storage Explorer] con il contenitore [!DNL Data Landing Zone].

![Riepilogo del contenitore utenti DLZ evidenziato nell&#39;interfaccia utente di Azure.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con il contenitore [!DNL Data Landing Zone] connesso a [!DNL Azure Storage Explorer], ora puoi iniziare a esportare i file da Experience Platform al contenitore [!DNL Data Landing Zone]. Per esportare i file, è necessario stabilire una connessione alla destinazione [!DNL Data Landing Zone] nell&#39;interfaccia utente di Experience Platform, come descritto nella sezione seguente.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Verificare di aver connesso il contenitore [!DNL Data Landing Zone] a [!DNL Azure Storage Explorer] come descritto nella sezione [prerequisiti](#prerequisites). Poiché [!DNL Data Landing Zone] è un archivio con provisioning Adobe, non è necessario eseguire ulteriori passaggi nell&#39;interfaccia utente Experience Platform per l&#39;autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
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

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

### Pianificazione

Nel passaggio **[!UICONTROL Pianificazione]**, puoi [impostare la pianificazione dell&#39;esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per la destinazione [!DNL Data Landing Zone] e [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

Nel passaggio **[!UICONTROL Mappatura]**, puoi selezionare l&#39;attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedi il [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell&#39;esercitazione dell&#39;interfaccia utente per l&#39;attivazione di destinazioni batch.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controllare l&#39;archivio [!DNL Data Landing Zone] e assicurarsi che i file esportati contengano le popolazioni di profilo previste.
