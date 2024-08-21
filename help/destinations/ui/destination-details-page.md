---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni;destination details page
title: Visualizzare i dettagli della destinazione
description: La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i tipi di pubblico mappati sulla destinazione e i controlli per modificare l’attivazione e abilitare e disabilitare il flusso di dati.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 47d0e2a7fae973edfda035d046f66c88d34bf8b2
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# Visualizzare i dettagli della destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli includono anche metriche per record di profilo attivati, identità attivate, non riuscite ed escluse e una cronologia delle esecuzioni dei flussi di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte dell&#39;area di lavoro [!UICONTROL Destinazioni] in [!DNL Platform] [!DNL UI]. Per ulteriori informazioni, consulta la panoramica dell&#39;area di lavoro [[!UICONTROL Destinazioni]](./destinations-workspace.md).

## Visualizzare i dettagli della destinazione {#view-details}

Per visualizzare ulteriori dettagli su una destinazione esistente, segui la procedura riportata di seguito. Puoi trovare l’ID di destinazione di una destinazione, l’utente che ha creato la destinazione, quando è stata creata e altre informazioni.

1. Accedi a [interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore per visualizzare le destinazioni esistenti.

   ![Sfoglia destinazioni](../assets/ui/details-page/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](../../images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/details-page/filter-destinations.png)

3. Seleziona la riga della destinazione per la quale desideri visualizzare ulteriori informazioni. Viene visualizzata una barra a destra con informazioni sulla destinazione, tra cui l’ID di destinazione, l’utente che ha creato la connessione di destinazione e altre informazioni.

   ![ID destinazione nella barra a destra](../assets/ui/details-page/right-rail-info-including-destination-id.png)

4. In alternativa, è possibile visualizzare altre informazioni sulla destinazione selezionando *il nome della destinazione* che si desidera visualizzare.

   ![Seleziona destinazione](../assets/ui/details-page/destination-select.png)

5. La pagina dei dettagli della destinazione viene visualizzata nella barra a destra, con i controlli disponibili.

   ![Dettagli destinazione](../assets/ui/details-page/destination-details.png)

## Barra a destra {#right-rail}

Nella barra a destra vengono visualizzate le informazioni di base sulla destinazione selezionata.

![barra a destra](../assets/ui/details-page/right-sidebar.png)

La tabella che segue riporta i controlli e i dettagli forniti dalla barra a destra:

| Elemento barra a destra | Descrizione |
| --- | --- |
| [!UICONTROL Attiva pubblico] | Selezionare questo controllo per modificare i tipi di pubblico mappati alla destinazione, aggiornare le pianificazioni di esportazione o aggiungere e rimuovere gli attributi e le identità mappati. Per ulteriori informazioni, consulta le guide su [attivazione dei dati sul pubblico nelle destinazioni di streaming del pubblico](./activate-segment-streaming-destinations.md), [attivazione dei dati sul pubblico nelle destinazioni basate su profili batch](./activate-batch-profile-destinations.md) e [attivazione dei dati sul pubblico nelle destinazioni basate su profili di streaming](./activate-streaming-profile-destinations.md). |
| [!UICONTROL Elimina] | Consente di eliminare questo flusso di dati e di annullare la mappatura dei tipi di pubblico precedentemente attivati, se presenti. |
| [!UICONTROL Nome destinazione] | Questo campo può essere modificato per aggiornare il nome della destinazione. |
| [!UICONTROL Descrizione] | Questo campo può essere modificato per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destinazione] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Per ulteriori informazioni, vedere il [catalogo delle destinazioni](../catalog/overview.md). |
| [!UICONTROL Stato] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Azioni di marketing] | Indica le azioni di marketing (casi di utilizzo) che si applicano a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Categoria] | Indica il tipo di destinazione. Per ulteriori informazioni, vedere il [catalogo delle destinazioni](../catalog/overview.md). |
| [!UICONTROL Tipo di connessione] | Indica il modulo tramite il quale i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Cookie] e [!UICONTROL Basato su profilo]. |
| [!UICONTROL Frequenza] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identità] | Rappresenta lo spazio dei nomi dell&#39;identità accettato dalla destinazione, ad esempio `GAID`, `IDFA` o `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, vedere la [panoramica dello spazio dei nomi di identità](../../identity-service/features/namespaces.md). |
| [!UICONTROL Creato da] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Creato] | Indica il datetime UTC al momento della creazione della destinazione. |

{style="table-layout:auto"}

## Attivazione/disattivazione di [!UICONTROL Enabled]/[!UICONTROL Disabled] {#enabled-disabled-toggle}

Puoi utilizzare l&#39;interruttore **[!UICONTROL Enabled]/[!UICONTROL Disabled]** per avviare e mettere in pausa tutte le esportazioni di dati nella destinazione.

![Attiva o disattiva flusso di dati](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Il flusso di dati viene eseguito] {#dataflow-runs}

La scheda [!UICONTROL Esecuzioni flusso di dati] fornisce dati metrici sul flusso di dati eseguito su destinazioni batch e di streaming. Per informazioni dettagliate e definizioni delle metriche, consultare [Flussi dati di monitoraggio](monitor-dataflows.md).

>[!NOTE]
>
>* La funzionalità di monitoraggio delle destinazioni è attualmente supportata per tutte le destinazioni nell&#39;Experience Platform *eccetto* le destinazioni [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) e [Tipi di pubblico Experienci Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md).
>* Per le destinazioni [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) e [HTTP API](/help/destinations/catalog/streaming/http-destination.md), vengono stimate le metriche relative alle identità escluse, non riuscite e attivate. Volumi più elevati di dati di attivazione consentono una maggiore precisione delle metriche.

![Il flusso di dati esegue la visualizzazione](../assets/ui/details-page/dataflow-runs.png)

### Durata esecuzioni flusso di dati {#dataflow-runs-duration}

Esiste una differenza nella durata visualizzata del flusso di dati eseguito tra lo streaming e le destinazioni basate su file.

### Destinazioni di streaming {#streaming}

Mentre la **[!UICONTROL durata elaborazione]** indicata per la maggior parte delle esecuzioni di flussi di dati è di circa quattro ore, come mostrato nell&#39;immagine seguente, il tempo di elaborazione effettivo per qualsiasi esecuzione di flussi di dati è molto più breve. Le finestre di esecuzione del flusso di dati rimangono aperte più a lungo nel caso in cui Experience Platform debba riprovare a effettuare chiamate alla destinazione e assicurarsi inoltre di non perdere dati in arrivo tardivo per la stessa finestra temporale.

![L&#39;immagine del flusso di dati esegue la pagina con la colonna Tempo di elaborazione evidenziata per una destinazione di streaming.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Per ulteriori informazioni, consulta le informazioni su [il flusso di dati viene eseguito su destinazioni di streaming](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nella documentazione di monitoraggio.

### Destinazioni basate su file {#file-based}

Per l&#39;esecuzione del flusso di dati in destinazioni basate su file, la **[!UICONTROL durata elaborazione]** dipende dalle dimensioni dei dati esportati e dal caricamento del sistema. Inoltre, il flusso di dati viene eseguito su destinazioni basate su file e viene suddiviso per pubblico.

![L&#39;immagine del flusso di dati esegue la pagina con la colonna Tempo di elaborazione evidenziata per una destinazione basata su file.](../assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Per ulteriori informazioni, leggere le informazioni su [il flusso di dati viene eseguito su destinazioni batch (basate su file)](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) nella documentazione di monitoraggio.

## [!UICONTROL Dati attivazione] {#activation-data}

Nella scheda **[!UICONTROL Dati attivazione]** viene visualizzato un elenco dei tipi di pubblico mappati sulla destinazione, inclusa la data di inizio e di fine (se applicabile) e altre informazioni rilevanti per l&#39;esportazione dei dati, come tipo di esportazione, pianificazione e frequenza. Per visualizzare i dettagli di un particolare pubblico, selezionane il nome dall’elenco.

>[!TIP]
>
>Per visualizzare e modificare i dettagli sugli attributi e le identità mappate a una destinazione, seleziona **[!UICONTROL Attiva pubblico]** nella [barra a destra](#right-rail).

>[!BEGINSHADEBOX]

Scheda **[!UICONTROL Dati attivazione]** per una destinazione basata su file.

![Destinazione batch visualizzazione dati attivazione](../assets/ui/details-page/activation-data-batch.png)

>[!ENDSHADEBOX]


>[!BEGINSHADEBOX]

Scheda **[!UICONTROL Dati attivazione]** per una destinazione di streaming.

![Destinazione streaming visualizzazione dati attivazione](../assets/ui/details-page/activation-data-streaming.png)

>[!ENDSHADEBOX]

### Filtrare i tipi di pubblico attivati {#filter-audiences}

Per filtrare l’elenco dei tipi di pubblico attivati per una destinazione, immetti un nome di pubblico nella casella di ricerca. L’elenco dei tipi di pubblico si aggiorna automaticamente con i risultati della ricerca.

![Casella di ricerca per filtrare i tipi di pubblico.](../assets/ui/details-page/filter-audiences.png)

### Rimuovere più tipi di pubblico dai flussi di attivazione {#bulk-remove}

Per rimuovere più tipi di pubblico dai flussi di attivazione esistenti, selezionare i tipi di pubblico, quindi selezionare **[!UICONTROL Rimuovi tipi di pubblico]**.

![Nella schermata dei dati di attivazione è evidenziata l&#39;opzione Rimuovi tipi di pubblico.](../assets/ui/details-page/bulk-remove-audiences.png)

### Esportare più file on-demand in destinazioni batch {#bulk-export}

Puoi [esportare più file on-demand](../ui/export-file-now.md) dalla pagina **[!UICONTROL Dati attivazione]**. A questo scopo, seleziona i tipi di pubblico per i quali desideri esportare i file su richiesta e seleziona il controllo **[!UICONTROL Esporta file ora]** per attivare un&#39;esportazione una tantum che distribuirà un file per ogni pubblico selezionato nella destinazione batch.

![Immagine che evidenzia il pulsante Esporta ora file.](../assets/ui/details-page/bulk-export-file-now.png)

### Modificare i programmi di attivazione per più tipi di pubblico esportati in destinazioni batch {#bulk-edit-schedule}

Per modificare la pianificazione di attivazione esistente di più tipi di pubblico contemporaneamente, selezionare i tipi di pubblico desiderati, quindi selezionare **[!UICONTROL Modifica pianificazione]**. Per informazioni dettagliate su come definire o modificare una pianificazione di esportazione, consulta la sezione [Pianifica esportazione pubblico](../ui/activate-batch-profile-destinations.md#scheduling).

![La schermata dei dati di attivazione evidenzia l&#39;opzione per modificare le pianificazioni di attivazione per più tipi di pubblico.](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;esplorazione della pagina dei dettagli di un pubblico, consulta la [panoramica di Audience Portal](../../segmentation/ui/audience-portal.md#segment-details).

### Modificare i nomi dei file per più tipi di pubblico esportati in destinazioni batch {#bulk-edit-file-names}

Per modificare contemporaneamente i nomi di file esportati di più tipi di pubblico, selezionare i tipi di pubblico desiderati, quindi selezionare **[!UICONTROL Modifica nome file]**. Per informazioni dettagliate su come definire o modificare un nome di file, leggere la sezione su come [configurare i nomi di file](../ui/activate-batch-profile-destinations.md#configure-file-names).

![La schermata dei dati di attivazione evidenzia l&#39;opzione di modifica dei nomi di file per più tipi di pubblico.](../assets/ui/details-page/bulk-edit-file-name.png)