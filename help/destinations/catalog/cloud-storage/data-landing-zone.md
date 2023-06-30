---
title: Destinazione Data Landing Zone
description: Scopri come connettersi alla Data Landing Zone per attivare segmenti ed esportare set di dati.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 5daa92b2f488b4acb825215f4da92af51bcf7c61
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%

---

# Destinazione Data Landing Zone (Beta)

>[!IMPORTANT]
>
>* Questa destinazione è attualmente in versione beta ed è disponibile solo per un numero limitato di clienti. Per richiedere l’accesso a [!DNL Data Landing Zone] connessione, contatta il tuo rappresentante di Adobe e fornisci [!DNL Organization ID].
>* Questa pagina della documentazione fa riferimento a [!DNL Data Landing Zone] *destinazione*. È inoltre disponibile un [!DNL Data Landing Zone] *sorgente* nel catalogo delle origini. Per ulteriori informazioni, leggere [[!DNL Data Landing Zone] sorgente](/help/sources/connectors/cloud-storage/data-landing-zone.md) documentazione.


## Panoramica {#overview}

[!DNL Data Landing Zone] è un [!DNL Azure Blob] l’interfaccia di archiviazione fornita da Adobe Experience Platform consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per esportare i file da Platform. Puoi accedervi [!DNL Data Landing Zone] contenitore per sandbox e il volume totale di dati in tutti i contenitori è limitato al totale dei dati forniti con la licenza Platform Products and Services. Tutti i clienti di Platform e dei relativi servizi applicativi, ad esempio [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services], e [!DNL Real-Time Customer Data Platform] dispongono di un [!DNL Data Landing Zone] contenitore per sandbox. Puoi leggere e scrivere file nel contenitore tramite [!DNL Azure Storage Explorer] o dall&#39;interfaccia della riga di comando.

[!DNL Data Landing Zone] supporta l&#39;autenticazione basata su SAS e i relativi dati sono protetti con [!DNL Azure Blob] meccanismi di sicurezza dello stoccaggio a riposo e in transito. L&#39;autenticazione basata su SAS consente di accedere in modo sicuro al [!DNL Data Landing Zone] tramite una connessione Internet pubblica. Non sono necessarie modifiche di rete per accedere al [!DNL Data Landing Zone] Contenitore, che significa che non è necessario configurare elenchi consentiti o configurazioni per più aree geografiche per la rete.

Platform applica un TTL (time-to-live) di sette giorni su tutti i file caricati in una [!DNL Data Landing Zone] contenitore. Tutti i file vengono eliminati dopo sette giorni.

## Connetti al tuo [!UICONTROL Data Landing Zone] archiviazione tramite API o interfaccia utente {#connect-api-or-ui}

* Per connettersi al tuo [!UICONTROL Data Landing Zone] percorso di archiviazione tramite l’interfaccia utente di Platform, leggi le sezioni [Connetti alla destinazione](#connect) e [Attiva i segmenti in questa destinazione](#activate) di seguito.
* Per connettersi al tuo [!UICONTROL Data Landing Zone] percorso di archiviazione a livello di programmazione, leggere [Attivare i segmenti in destinazioni basate su file utilizzando l’esercitazione API del servizio Flow](../../api/activate-segments-file-based-destinations.md).

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema applicabili (ad esempio il tuo PPID), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni su [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Prima di poter utilizzare il [!DNL Data Landing Zone] destinazione.

### Connetti [!DNL Data Landing Zone] contenitore a [!DNL Azure Storage Explorer]

È possibile utilizzare [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) per gestire il contenuto del [!DNL Data Landing Zone] contenitore. Per iniziare a utilizzare [!DNL Data Landing Zone], devi prima recuperare le credenziali, inserirle in [!DNL Azure Storage Explorer], e collegare [!DNL Data Landing Zone] contenitore a [!DNL Azure Storage Explorer].

In [!DNL Azure Storage Explorer] UI, seleziona l’icona della connessione nella barra di navigazione a sinistra. Il **Seleziona risorsa** viene visualizzata una finestra che fornisce le opzioni per la connessione. Seleziona **[!DNL Blob container]** per connettersi al tuo [!DNL Data Landing Zone] archiviazione.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Quindi, seleziona **URL firma di accesso condiviso (SAS)** come metodo di connessione e quindi selezionare **Successivo**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

Dopo aver selezionato il metodo di connessione, devi fornire un **nome visualizzato** e **[!DNL Blob]URL SAS contenitore** che corrisponde al tuo [!DNL Data Landing Zone] contenitore.

>[!BEGINSHADEBOX]

### Recupera le credenziali per [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Devi utilizzare le API di Platform per recuperare [!DNL Data Landing Zone] credenziali. La chiamata API per recuperare le credenziali è descritta di seguito. Per informazioni su come ottenere i valori richiesti per le intestazioni, consulta [Guida introduttiva alle API di Adobe Experience Platform](/help/landing/api-guide.md) guida.

**Formato API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Parametri query | Descrizione |
| --- | --- |
| `dlz_destination` | Il `dlz_destination` Il tipo consente all’API di distinguere un contenitore di destinazione di una zona di destinazione dagli altri tipi di contenitori disponibili. |

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

La risposta seguente restituisce le informazioni sulle credenziali per la zona di destinazione, incluso l’attuale `SASToken` e `SASUri`e `storageAccountName` che corrisponde al contenitore della zona di destinazione.

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

### Aggiorna [!DNL Data Landing Zone] credenziali {#update-dlz-credentials}

Se necessario, puoi anche aggiornare le credenziali. È possibile aggiornare `SASToken` facendo una richiesta POST al `/credentials` endpoint del [!DNL Connectors] API.

**Formato API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Parametri query | Descrizione |
| --- | --- |
| `dlz_destination` | Il `dlz_destination` Il tipo consente all’API di distinguere un contenitore di destinazione di una zona di destinazione dagli altri tipi di contenitori disponibili. |
| `refresh` | Il `refresh` consente di reimpostare le credenziali della zona di destinazione e generare automaticamente un nuovo `SASToken`. |

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

La seguente risposta restituisce valori aggiornati per il `SASToken` e `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Immetti il nome visualizzato (`containerName`) e [!DNL Data Landing Zone] URL SAS, come restituito nella chiamata API descritta in precedenza, quindi selezionare **Successivo**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Il **Riepilogo** viene visualizzata una finestra che fornisce una panoramica delle impostazioni, incluse informazioni [!DNL Blob] endpoint e autorizzazioni. Quando è pronto, seleziona **Connetti**.

![riepilogo](/help/sources/images/tutorials/create/dlz/summary.png)

Una connessione corretta aggiorna il tuo [!DNL Azure Storage Explorer] Interfaccia utente con [!DNL Data Landing Zone] contenitore.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Con [!DNL Data Landing Zone] contenitore connesso a [!DNL Azure Storage Explorer], ora puoi iniziare a esportare i file da Experience Platform al tuo [!DNL Data Landing Zone] contenitore. Per esportare i file, è necessario stabilire una connessione con [!DNL Data Landing Zone] nell’interfaccia utente di Experience Platform, come descritto nella sezione seguente.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Assicurarsi di aver connesso [!DNL Data Landing Zone] contenitore a [!DNL Azure Storage Explorer] come descritto nella [prerequisiti](#prerequisites) sezione. Perché [!DNL Data Landing Zone] è un archivio con provisioning Adobe, non è necessario eseguire ulteriori passaggi nell’interfaccia utente Experience Platform per l’autenticazione nella destinazione.

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di file]**: seleziona l’Experience Platform di formato da utilizzare per i file esportati. Quando si seleziona [!UICONTROL CSV] , è inoltre possibile [configurare le opzioni di formattazione del file](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Formato di compressione]**: seleziona il tipo di compressione che Experience Platform deve utilizzare per i file esportati.
* **[!UICONTROL Includi file manifesto]**: attiva questa opzione se desideri che le esportazioni includano un file JSON manifesto che contiene informazioni sulla posizione di esportazione, sulle dimensioni di esportazione e altro ancora.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Pianificazione

In **[!UICONTROL Pianificazione]** passaggio, puoi [impostare la pianificazione di esportazione](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) per [!DNL Data Landing Zone] e puoi anche [configurare il nome dei file esportati](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappare attributi e identità {#map}

In **[!UICONTROL Mappatura]** fase, puoi selezionare l’attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedere [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell’esercitazione dell’interfaccia utente attiva destinazioni batch.

## (Beta) Esportare i set di dati {#export-datasets}

Questa destinazione supporta le esportazioni di set di dati. Per informazioni complete su come impostare le esportazioni dei set di dati, consulta le esercitazioni:

* Procedura [esportare i set di dati utilizzando l’interfaccia utente di Platform](/help/destinations/ui/export-datasets.md).
* Procedura [esportare i set di dati a livello di programmazione utilizzando l’API del servizio Flusso](/help/destinations/api/export-datasets.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente, controlla [!DNL Data Landing Zone] e assicurati che i file esportati contengano le popolazioni di profilo previste.
