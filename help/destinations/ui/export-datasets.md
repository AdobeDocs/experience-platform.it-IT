---
title: Esportare i set di dati nelle destinazioni di archiviazione cloud
type: Tutorial
description: Scopri come esportare i set di dati da Adobe Experience Platform nella posizione di archiviazione cloud preferita.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: d6b3dd7de1e8b5247bf692d1654fc4506ab4a471
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 4%

---

# Esportare i set di dati nelle destinazioni dell’archiviazione cloud

>[!AVAILABILITY]
>
>* Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime o Ultimate, Adobe Journey Optimizer o il Customer Journey Analytics. Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.

Questo articolo spiega il flusso di lavoro necessario per esportare [set di dati](/help/catalog/datasets/overview.md) da Adobe Experience Platform alla posizione di archiviazione cloud preferita, ad esempio [!DNL Amazon S3], posizioni SFTP o [!DNL Google Cloud Storage] utilizzando l’interfaccia utente di Experienci Platform.

Puoi anche utilizzare le API Experienci Platform per esportare i set di dati. Leggi le [esercitazione sull’API per l’esportazione di set di dati](/help/destinations/api/export-datasets.md) per ulteriori informazioni.

## Set di dati disponibili per l’esportazione {#datasets-to-export}

I set di dati che puoi esportare variano in base all’applicazione di Experience Platform (Real-Time CDP, Adobe Journey Optimizer), al livello (Prime o Ultimate) ed eventuali componenti aggiuntivi acquistati (ad esempio, Data Distiller).

Scopri dalla tabella seguente quali tipi di set di dati puoi esportare in base all’applicazione, al livello di prodotto ed eventuali componenti aggiuntivi acquistati:

<table>
<thead>
  <tr>
    <th>Applicazione/componente aggiuntivo</th>
    <th>Livello</th>
    <th>Set di dati disponibili per l’esportazione</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experienci Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audienci Manager.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experienci Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audienci Manager.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Set di dati snapshot del profilo generato dal sistema</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Consulta la sezione <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentazione.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Consulta la sezione <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Adobe Journey Optimizer</a> documentazione.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Tutto</td>
    <td> <p> Set di dati di profili ed eventi di esperienza creati nell’interfaccia utente di Experienci Platform dopo l’acquisizione o la raccolta di dati tramite Sources, Web SDK, Mobile SDK, Analytics Data Connector ed Audienci Manager. Scopri le autorizzazioni richieste in <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/cja-access-control.html#product-admin-additional-permissions"> Documentazione del Customer Journey Analytics</a>. </p> <p> <b>Nota sulla disponibilità:</b> La possibilità di esportare i set di dati nel cloud si trova nella fase di test limitato del rilascio e potrebbe non essere ancora disponibile nell’ambiente. Questa nota verrà rimossa non appena la funzionalità sarà disponibile a livello generale. Per informazioni sulla procedura di rilascio del Customer Journey Analytics, consulta <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/releases/releases.html"> Rilasci di funzioni del Customer Journey Analytics</a>. </p> </td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Data Distiller (componente aggiuntivo)</td>
    <td>Set di dati derivati creati tramite Query Service.</td>
  </tr>
</tbody>
</table>

## Esercitazione video {#video-tutorial}

Guarda il video seguente per una spiegazione end-to-end del flusso di lavoro descritto in questa pagina, i vantaggi dell’utilizzo della funzionalità di esportazione dei set di dati e alcuni casi d’uso consigliati.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Destinazioni supportati {#supported-destinations}

Al momento, puoi esportare i set di dati nelle destinazioni di archiviazione cloud evidenziate nella schermata ed elencate di seguito.

![Pagina del catalogo delle destinazioni che mostra quali destinazioni supportano le esportazioni dei set di dati.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Quando attivare tipi di pubblico o esportare set di dati {#when-to-activate-audiences-or-activate-datasets}

Alcune destinazioni basate su file nel catalogo Experienci Platform supportano sia l’attivazione del pubblico che l’esportazione di set di dati.

* Considera l’attivazione di tipi di pubblico quando desideri che i dati siano strutturati in profili raggruppati per interessi o qualifiche di pubblico.
* In alternativa, puoi prendere in considerazione le esportazioni di set di dati quando desideri esportare set di dati non elaborati, che non sono raggruppati o strutturati in base agli interessi o alle qualifiche del pubblico. Puoi utilizzare questi dati per reporting, flussi di lavoro sulla scienza dei dati e molti altri casi d’uso. In qualità di amministratore, ingegnere dati o analista, ad esempio, puoi esportare i dati da Experienci Platform per sincronizzarli con il data warehouse, utilizzarli in strumenti di analisi BI, in strumenti di ML cloud esterni o archiviarli nel sistema per esigenze di archiviazione a lungo termine.

Questo documento contiene tutte le informazioni necessarie per esportare i set di dati. Se desideri attivare *audience* nelle destinazioni del marketing via e-mail o dell’archiviazione cloud, leggi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md).

## Prerequisiti {#prerequisites}

Per esportare i set di dati nelle destinazioni di archiviazione cloud, è necessario disporre di [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, accedi al [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

### Autorizzazioni necessarie {#permissions}

Per esportare i set di dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Visualizzare i set di dati]**, e **[!UICONTROL Gestire e attivare le destinazioni dei set di dati]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per assicurarti di disporre delle autorizzazioni necessarie per esportare i set di dati e che la destinazione supporti l’esportazione dei set di dati, sfoglia il catalogo delle destinazioni. Se una destinazione ha **[!UICONTROL Attiva]** o un **[!UICONTROL Esportare i set di dati]** , quindi si dispone delle autorizzazioni appropriate.

## Seleziona la destinazione {#select-destination}

Segui le istruzioni per selezionare una destinazione in cui puoi esportare i set di dati:

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda.

   ![Scheda Catalogo di destinazione con il controllo Catalogo evidenziato.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva]** o **[!UICONTROL Esportare i set di dati]** nella scheda corrispondente alla destinazione in cui desideri esportare i set di dati.

   ![Scheda Catalogo di destinazione con il controllo Attiva evidenziato.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Seleziona **[!UICONTROL Tipo di dati Set di dati]** e seleziona la connessione di destinazione in cui desideri esportare i set di dati, quindi seleziona **[!UICONTROL Successivo]**.

>[!TIP]
> 
>Se desideri impostare una nuova destinazione per l’esportazione dei set di dati, seleziona **[!UICONTROL Configurare una nuova destinazione]** per attivare [Connetti alla destinazione](/help/destinations/ui/connect-destination.md) flusso di lavoro.

![Flusso di lavoro di attivazione della destinazione con il controllo Set di dati evidenziato.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Il **[!UICONTROL Seleziona set di dati]** viene visualizzata. Procedi alla sezione successiva per [seleziona i set di dati](#select-datasets) per l&#39;esportazione.

## Seleziona i set di dati {#select-datasets}

Utilizza le caselle di controllo a sinistra dei nomi dei set di dati per selezionare i set di dati da esportare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio Seleziona set di dati in cui puoi selezionare i set di dati da esportare.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Pianificare l’esportazione di set di dati {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Opzioni di esportazione dei file per i set di dati"
>abstract="Seleziona **Esporta file incrementali** per esportare solo i dati aggiunti al set di dati dopo l’ultima esportazione. <br> La prima esportazione di file incrementali include tutti i dati del set di dati, agendo come backfill. I file incrementali futuri includono solo i dati aggiunti al set di dati dopo la prima esportazione."

In **[!UICONTROL Pianificazione]** passaggio, puoi impostare una data di inizio e una cadenza di esportazione per le esportazioni dei set di dati.

Il **[!UICONTROL Esporta file incrementali]** viene selezionata automaticamente. Questo attiva un’esportazione di uno o più file che rappresentano un’istantanea completa del set di dati. I file successivi sono aggiunte incrementali al set di dati dall’esportazione precedente.

>[!IMPORTANT]
>
>La prima esportazione incrementale di file include tutti i dati esistenti nel set di dati, che funziona come retrocompilazione. L’esportazione può contenere uno o più file.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio di pianificazione.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Utilizza il **[!UICONTROL Frequenza]** per selezionare la frequenza di esportazione:

   * **[!UICONTROL Giornaliero]**: pianifica le esportazioni di file incrementali una volta al giorno, ogni giorno, all’ora specificata.
   * **[!UICONTROL Ogni ora]**: pianifica le esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

2. Utilizza il **[!UICONTROL Ora]** per scegliere l’ora del giorno, in [!DNL UTC] , quando deve essere effettuata l&#39;esportazione.

3. Utilizza il **[!UICONTROL Data]** per scegliere l&#39;intervallo di esecuzione dell&#39;esportazione. Al momento non è possibile impostare una data di fine per le esportazioni. Per ulteriori informazioni, vedere [limitazioni note](#known-limitations) sezione.

4. Seleziona **[!UICONTROL Successivo]** per salvare la pianificazione e passare alla **[!UICONTROL Revisione]** passaggio.

>[!NOTE]
> 
>Per le esportazioni di set di dati, i nomi dei file hanno un formato predefinito, predefinito, che non può essere modificato. Consulta la sezione [Verificare l’esportazione del set di dati](#verify) per ulteriori informazioni ed esempi di file esportati.

## Revisione {#review}

Il giorno **[!UICONTROL Revisione]** pagina, è possibile visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a esportare i set di dati nella destinazione.

![Flusso di lavoro di esportazione del set di dati che mostra il passaggio di revisione.](/help/destinations/assets/ui/export-datasets/review.png)

## Verificare l’esportazione del set di dati {#verify}

Durante l’esportazione dei set di dati, in Experienci Platform ne vengono creati uno o più `.json` o `.parquet` file nel percorso di archiviazione fornito. I nuovi file verranno archiviati nel percorso di archiviazione in base alla pianificazione di esportazione fornita.

In Experience Platform viene creata una struttura di cartelle nel percorso di archiviazione specificato, in cui vengono depositati i file del set di dati esportati. Per ogni esportazione viene creata una nuova cartella, seguendo il modello riportato di seguito:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Il nome di file predefinito viene generato in modo casuale e garantisce che i nomi di file esportati siano univoci.

### File di set di dati di esempio {#sample-files}

La presenza di questi file nel percorso di archiviazione conferma la riuscita dell’esportazione. Per comprendere come sono strutturati i file esportati, puoi scaricare un esempio [file .parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet) o [file .json](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json).

#### File di set di dati compressi {#compressed-dataset-files}

In [connetti al flusso di lavoro di destinazione](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options), puoi selezionare i file del set di dati esportati da comprimere, come illustrato di seguito:

![Tipo di file e selezione della compressione durante la connessione a una destinazione per esportare i set di dati.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Quando vengono compressi, si noti la differenza di formato tra i due tipi di file:

* Durante l’esportazione di file JSON compressi, il formato del file esportato è `json.gz`
* Quando si esportano file parquet compressi, il formato di file esportato è `gz.parquet`

## Rimuovi set di dati dalla destinazione {#remove-dataset}

Per rimuovere un set di dati da un flusso di dati esistente, effettua le seguenti operazioni:

1. Accedi a [Interfaccia utente Experienci Platform](https://experience.adobe.com/platform/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione in alto per visualizzare i flussi di dati di destinazione esistenti.

   ![Visualizzazione Sfoglia destinazione con una connessione di destinazione visualizzata e il resto sfocato.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Seleziona l’icona del filtro ![Icona filtro](../assets/ui/edit-activation/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

1. Dalla sezione **[!UICONTROL Dati di attivazione]** , selezionare il controllo set di dati per visualizzare tutti i set di dati mappati a questo flusso di dati di esportazione.

   ![L’opzione di navigazione dei set di dati disponibili è evidenziata nella colonna Dati di attivazione.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. Il **[!UICONTROL Dati di attivazione]** viene visualizzata la pagina della destinazione. Seleziona **[!UICONTROL Rimuovi set di dati]** nella barra a destra per attivare la finestra di dialogo rimuovi conferma set di dati.

   ![Finestra di dialogo Rimuovi set di dati che mostra il controllo Rimuovi set di dati nella barra a destra.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Nella finestra di dialogo di conferma, seleziona **[!UICONTROL Rimuovi]** per rimuovere immediatamente il set di dati dalle esportazioni nella destinazione.

   ![Finestra di dialogo che mostra l’opzione Conferma rimozione set di dati dal flusso di dati.](../assets/ui/export-datasets/remove-dataset-confirm.png)


## Diritti di esportazione del set di dati {#licensing-entitlement}

Consulta i documenti di descrizione del prodotto per capire la quantità di dati che hai diritto di esportare per ogni applicazione di Experience Platform all’anno. Ad esempio, puoi visualizzare la descrizione del prodotto Real-Time CDP [qui](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

I diritti all’esportazione di dati per diverse applicazioni non sono additivi. Ciò significa, ad esempio, che se acquisti Real-Time CDP Ultimate e Adobe Journey Optimizer Ultimate, il diritto all’esportazione del profilo sarà il più grande tra i due diritti, in base alle descrizioni del prodotto. Il volume di adesioni viene calcolato moltiplicando il numero totale di profili con licenza per 500 KB per Real-Time CDP Prime o 700 KB per Real-Time CDP Ultimate per determinare il volume di dati a cui hai diritto.

Se invece sono stati acquistati componenti aggiuntivi come Data Distiller, il limite di esportazione dei dati a cui hai diritto rappresenta la somma del livello prodotto e del componente aggiuntivo.

Puoi visualizzare e tenere traccia delle esportazioni di profili in base ai limiti contrattuali nel dashboard delle licenze.

## Limitazioni note {#known-limitations}

Tieni presente le seguenti limitazioni per il rilascio di disponibilità generale delle esportazioni di set di dati:

* Attualmente, è possibile esportare solo file incrementali e non è possibile selezionare una data di fine per le esportazioni dei set di dati.
* I nomi di file esportati non sono attualmente personalizzabili.
* I set di dati creati tramite API non sono attualmente disponibili per l’esportazione.
* L’interfaccia utente non ti blocca attualmente l’eliminazione di un set di dati in fase di esportazione in una destinazione. Non eliminare i set di dati da esportare nelle destinazioni. [Rimuovi il set di dati](#remove-dataset) da un flusso di dati di destinazione prima di eliminarlo.
* Le metriche di monitoraggio per le esportazioni di set di dati sono attualmente combinate con i numeri per le esportazioni di profili, pertanto non riflettono i numeri di esportazione effettivi.
