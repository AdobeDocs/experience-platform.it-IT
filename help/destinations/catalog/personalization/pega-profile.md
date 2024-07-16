---
title: Connettore profilo Pega
description: Utilizza il connettore di profilo Pega per Amazon S3 in Adobe Experience Platform per esportare dati di profilo completi o incrementali, o entrambi, nell’archiviazione cloud Amazon S3. In Pega Customer Decision Hub, è possibile pianificare i processi di dati in Customer Profile Designer per importare periodicamente i dati del profilo dallo storage Amazon S3.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 4%

---

# Connettore profilo Pega

## Panoramica {#overview}

Utilizza [!DNL Pega Profile Connector] in Adobe Experience Platform per creare una connessione in uscita in tempo reale all&#39;archiviazione [!DNL Amazon Web Services] (AWS) S3 per esportare periodicamente i dati del profilo in file CSV da Adobe Experience Platform nei tuoi bucket S3. In [!DNL Pega Customer Decision Hub], è possibile pianificare processi di dati per importare questi dati profilo dall’archiviazione S3 per aggiornare il profilo di [!DNL Pega Customer Decision Hub].

Questo connettore consente di configurare l&#39;esportazione iniziale dei dati del profilo e di sincronizzare periodicamente nuovi profili in [!DNL Pega Customer Decision Hub].  La disponibilità di dati aggiornati nell’hub decisionale del cliente fornisce una visualizzazione migliore e aggiornata della base clienti per le decisioni ottimali successive.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da Pegasystems. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Pega [qui](mailto:support@pega.com).

## Casi d’uso

Per capire meglio come e quando utilizzare la destinazione [!DNL Pega Profile Connector], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d’uso 1

Un addetto marketing desidera configurare inizialmente [!DNL Pega Customer Decision Hub] con i dati del profilo caricati da Adobe Experience Platform. Si tratta di un carico completo iniziale seguito da carichi delta su base pianificata.

### Caso d’uso 2

Un addetto al marketing desidera che in [!DNL Pega Customer Decision Hub] siano disponibili dati di profilo aggiornati da Adobe Experience Platform, in modo da poter migliorare costantemente le informazioni Pega sui profili dei clienti.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare questa destinazione per esportare i dati da Adobe Experience Platform e importare i profili in [!DNL Pega Customer Decision Hub], è necessario soddisfare i seguenti prerequisiti:

* Configurare il bucket [!DNL Amazon S3] e il percorso della cartella da utilizzare per l&#39;esportazione e l&#39;importazione di file di dati.
* Configurare la chiave di accesso [!DNL Amazon S3] e la chiave segreta [!DNL Amazon S3]: In [!DNL Amazon S3], generare una coppia `access key - secret access key` per concedere l&#39;accesso Platform all&#39;account [!DNL Amazon S3].
* Per connettere ed esportare correttamente i dati nel percorso di archiviazione [!DNL Amazon S3], creare un utente di Gestione identità e accesso (IAM) per [!DNL Platform] in [!DNL Amazon S3] e assegnare autorizzazioni quali `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Assicurarsi che l&#39;istanza [!DNL Pega Customer Decision Hub] sia aggiornata alla versione 8.8 o successiva.

## Identità supportate {#supported-identities}

[!DNL Pega Customer Decision Hub] supporta l&#39;attivazione degli ID utente personalizzati descritti nella tabella seguente. Per ulteriori dettagli, vedi [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| *IDCliente* | Identificatore utente comune che identifica in modo univoco un profilo in [!DNL Pega Customer Decision Hub] e Adobe Experience Platform |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Le destinazioni batch esportano i file sulle piattaforme a valle con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* Chiave di accesso **[!DNL Amazon S3]** e chiave segreta **[!DNL Amazon S3]**: in [!DNL Amazon S3], genera una coppia `access key - secret access key` per concedere l&#39;accesso Adobe Experience Platform al tuo account [!DNL Amazon S3]. Ulteriori informazioni sono disponibili nella [documentazione di Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Inserire i dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione a [!DNL Amazon S3], fornire le seguenti informazioni per la destinazione:

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli di destinazione del connettore profilo Pega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Per configurare i dettagli per la destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Successivo]**. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immettere un nome che consenta di identificare la destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Nome bucket]**: immettere il nome del bucket [!DNL Amazon S3] da utilizzare per questa destinazione.
* **[!UICONTROL Percorso cartella]**: immettere il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Tipo di compressione]**: selezionare il tipo di compressione GZIP o NONE.

>[!TIP]
>
>Nel flusso di lavoro della destinazione di connessione, puoi creare una cartella personalizzata nell’archiviazione Amazon S3 per file di pubblico esportato. Per istruzioni, leggere [Utilizzare le macro per creare una cartella nel percorso di archiviazione](/help/destinations/catalog/cloud-storage/overview.md#use-macros).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione profilo batch](../../ui/activate-batch-profile-destinations.md).

### Mappare attributi e identità {#map}

Nel passaggio **[!UICONTROL Mappatura]**, puoi selezionare l&#39;attributo e i campi di identità da esportare per i profili. Puoi anche scegliere di modificare le intestazioni nel file esportato con qualsiasi nome descrittivo. Per ulteriori informazioni, vedi il [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) nell&#39;esercitazione dell&#39;interfaccia utente per l&#39;attivazione di destinazioni batch.

## Convalidare l’esportazione dei dati {#exported-data}

Per [!DNL Pega Profile Connector] destinazioni, [!DNL Platform] crea un file `.csv` nel percorso di archiviazione Amazon S3 fornito. Per ulteriori informazioni sui file, vedere [Attivare i dati del pubblico nelle destinazioni di esportazione dei profili batch](../../ui/activate-batch-profile-destinations.md) nell&#39;esercitazione di attivazione del pubblico.

Importazione dei dati di profilo da S3 completata. I dati vengono inseriti nell&#39;archivio dati di profilo [!DNL Pega Customer]. I dati importati del profilo cliente possono essere convalidati in [!DNL Pega Customer Profile Designer], come illustrato nella figura seguente.
![Immagine della schermata dell&#39;interfaccia utente in cui è possibile convalidare i dati del profilo di Adobe nel profilo cliente Designer](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

In [!DNL Pega Customer Decision Hub], gli amministratori di dati possono configurare processi di dati in [!DNL Customer Profile Designer] per importare periodicamente i dati del profilo da S3, come illustrato nella figura seguente. Per ulteriori informazioni su come configurare i processi di dati per importare i dati del profilo da [!DNL Amazon S3], vedere [risorse aggiuntive](#additional-resources).
![Immagine della schermata dell&#39;interfaccia utente per configurare i processi di dati nel profilo cliente Designer](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Risorse aggiuntive {#additional-resources}

Vedi [Processi di importazione dati](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
