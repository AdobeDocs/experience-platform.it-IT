---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni;destination details page
title: Visualizzare i dettagli della destinazione
description: La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i tipi di pubblico mappati sulla destinazione e i controlli per modificare l’attivazione e abilitare e disabilitare il flusso di dati.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---

# Visualizzare i dettagli della destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli includono anche metriche per record di profilo attivati, identità attivate, non riuscite ed escluse e una cronologia delle esecuzioni dei flussi di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte della sezione [!UICONTROL Destinazioni] area di lavoro in [!DNL Platform] [!DNL UI]. Consulta la [[!UICONTROL Destinazioni] panoramica di workspace](./destinations-workspace.md) per ulteriori informazioni.

## Visualizzare i dettagli della destinazione {#view-details}

Per visualizzare ulteriori dettagli su una destinazione esistente, segui la procedura riportata di seguito.

1. Accedi a [Interfaccia utente Experienci Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione in alto per visualizzare le destinazioni esistenti.

   ![Sfoglia destinazioni](../assets/ui/details-page/browse-destinations.png)

1. Seleziona l’icona del filtro ![Icona filtro](../assets/ui/details-page/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/details-page/filter-destinations.png)

1. Seleziona il nome della destinazione da visualizzare.

   ![Seleziona destinazione](../assets/ui/details-page/destination-select.png)

1. Viene visualizzata la pagina dei dettagli della destinazione, con i controlli disponibili.

   ![Dettagli della destinazione](../assets/ui/details-page/destination-details.png)

## Barra a destra {#right-rail}

Nella barra a destra vengono visualizzate le informazioni di base sulla destinazione selezionata.

![barra a destra](../assets/ui/details-page/right-sidebar.png)

La tabella che segue riporta i controlli e i dettagli forniti dalla barra a destra:

| Elemento barra a destra | Descrizione |
| --- | --- |
| [!UICONTROL Attiva tipi di pubblico] | Selezionare questo controllo per modificare i tipi di pubblico mappati alla destinazione, aggiornare le pianificazioni di esportazione o aggiungere e rimuovere gli attributi e le identità mappati. Consulta le guide su [attivazione dei dati sul pubblico nelle destinazioni di streaming del pubblico](./activate-segment-streaming-destinations.md), [attivazione dei dati sul pubblico in destinazioni basate su profili batch](./activate-batch-profile-destinations.md), e [attivazione dei dati sul pubblico per lo streaming di destinazioni basate su profili](./activate-streaming-profile-destinations.md) per ulteriori informazioni. |
| [!UICONTROL Elimina] | Consente di eliminare questo flusso di dati e di annullare la mappatura dei tipi di pubblico precedentemente attivati, se presenti. |
| [!UICONTROL Nome destinazione] | Questo campo può essere modificato per aggiornare il nome della destinazione. |
| [!UICONTROL Descrizione] | Questo campo può essere modificato per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destinazione] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Consulta la [catalogo delle destinazioni](../catalog/overview.md) per ulteriori informazioni. |
| [!UICONTROL Stato] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Azioni di marketing] | Indica le azioni di marketing (casi di utilizzo) che si applicano a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Categoria] | Indica il tipo di destinazione. Consulta la [catalogo delle destinazioni](../catalog/overview.md) per ulteriori informazioni. |
| [!UICONTROL Tipo di connessione] | Indica il modulo tramite il quale i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Cookie] e [!UICONTROL Basato su profilo]. |
| [!UICONTROL Frequenza] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identità] | Rappresenta lo spazio dei nomi delle identità accettato dalla destinazione, ad esempio `GAID`, `IDFA`, o `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, vedi [panoramica dello spazio dei nomi delle identità](../../identity-service/features/namespaces.md). |
| [!UICONTROL Creato da] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Creato] | Indica il datetime UTC al momento della creazione della destinazione. |

{style="table-layout:auto"}

## [!UICONTROL Abilitato]/[!UICONTROL Disabilitato] attivare/disattivare {#enabled-disabled-toggle}

È possibile utilizzare **[!UICONTROL Abilitato]/[!UICONTROL Disabilitato]** attiva per avviare e mettere in pausa tutte le esportazioni di dati nella destinazione.

![Attiva o disattiva il flusso di dati](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Il flusso di dati viene eseguito] {#dataflow-runs}

Il [!UICONTROL Il flusso di dati viene eseguito] fornisce i dati delle metriche sul flusso di dati eseguito su destinazioni in batch e in streaming. Fai riferimento a [Monitorare i flussi di dati](monitor-dataflows.md) per dettagli e definizioni di metriche.

>[!NOTE]
>
>* La funzionalità di monitoraggio delle destinazioni è attualmente supportata per tutte le destinazioni in Experienci Platform *eccetto* il [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) e [Tipi di pubblico di Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinazioni.
>* Per [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Hub eventi di Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), e [API HTTP](/help/destinations/catalog/streaming/http-destination.md) destinazioni, vengono stimate le metriche relative alle identità escluse, non riuscite e attivate. Volumi più elevati di dati di attivazione consentono una maggiore precisione delle metriche.

![Visualizzazione esecuzioni flusso di dati](../assets/ui/details-page/dataflow-runs.png)

### Durata esecuzioni flusso di dati {#dataflow-runs-duration}

Esiste una differenza nella durata visualizzata del flusso di dati eseguito tra lo streaming e le destinazioni basate su file.

### Destinazioni di streaming {#streaming}

Mentre il **[!UICONTROL Durata di elaborazione]** indicato per la maggior parte delle esecuzioni di flussi di dati in streaming è di circa quattro ore, come mostrato nell’immagine seguente, il tempo di elaborazione effettivo per qualsiasi esecuzione di flussi di dati è molto più breve. Le finestre di esecuzione del flusso di dati rimangono aperte più a lungo nel caso in cui Experienci Platform debba riprovare a effettuare chiamate alla destinazione e assicurarsi inoltre di non perdere dati in arrivo tardivo per la stessa finestra temporale.

![Immagine del flusso di dati esegue la pagina con la colonna Tempo di elaborazione evidenziata per una destinazione di streaming.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Per ulteriori informazioni, consulta [il flusso di dati viene eseguito sulle destinazioni di streaming](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nella documentazione di monitoraggio.

### Destinazioni basate su file {#file-based}

Per eseguire il flusso di dati su destinazioni basate su file, il **[!UICONTROL Durata di elaborazione]** dipende dalle dimensioni dei dati esportati e dal caricamento del sistema. Inoltre, il flusso di dati viene eseguito su destinazioni basate su file e viene suddiviso per pubblico.

![Immagine del flusso di dati esegue la pagina con la colonna Tempo di elaborazione evidenziata per una destinazione basata su file.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Per ulteriori informazioni, consulta [il flusso di dati viene eseguito su destinazioni batch (basate su file)](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) nella documentazione di monitoraggio.

## [!UICONTROL Dati di attivazione] {#activation-data}

Il [!UICONTROL Dati di attivazione] Nella scheda viene visualizzato un elenco dei tipi di pubblico mappati sulla destinazione, che include la data di inizio e la data di fine (se applicabili) e altre informazioni rilevanti per l’esportazione dei dati, come il tipo, la pianificazione e la frequenza dell’esportazione. Per visualizzare i dettagli di un particolare pubblico, selezionane il nome dall’elenco.

>[!TIP]
>
>Per visualizzare e modificare i dettagli degli attributi e delle identità mappati a una destinazione, seleziona **[!UICONTROL Attiva tipi di pubblico]** nel [barra a destra](#right-rail).

![Destinazione batch della visualizzazione dati di attivazione](../assets/ui/details-page/activation-data-batch.png)

![Destinazione streaming visualizzazione dati di attivazione](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Per informazioni dettagliate sull’esplorazione della pagina dei dettagli di un pubblico, consulta [Panoramica sulla segmentazione dell’interfaccia utente](../../segmentation/ui/overview.md#segment-details).
