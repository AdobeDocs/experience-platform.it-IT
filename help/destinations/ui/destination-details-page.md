---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni
title: Visualizza dettagli destinazione
description: La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a84d67e433d70cc6194ca20abc656e4b141d42a6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Visualizza dettagli destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli includono anche le metriche per i record di profilo attivati, le identità attivate, non riuscite ed escluse e una cronologia delle esecuzioni del flusso di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte del [!UICONTROL Destinazioni] nell&#39;area di lavoro [!DNL Platform] [!DNL UI]. Consulta la sezione [[!UICONTROL Destinazioni] panoramica dell&#39;area di lavoro](./destinations-workspace.md) per ulteriori informazioni.

## Visualizza dettagli destinazione {#view-details}

Segui i passaggi riportati di seguito per visualizzare ulteriori dettagli su una destinazione esistente.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione superiore per visualizzare le destinazioni esistenti.

   ![Sfoglia destinazioni](../assets/ui/details-page/browse-destinations.png)

1. Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/details-page/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/details-page/filter-destinations.png)

1. Selezionare il nome della destinazione che si desidera visualizzare.

   ![Seleziona destinazione](../assets/ui/details-page/destination-select.png)

1. Viene visualizzata la pagina dei dettagli della destinazione, con i relativi controlli disponibili.

   ![Dettagli della destinazione](../assets/ui/details-page/destination-details.png)

## Barra a destra {#right-rail}

Nella barra a destra sono visualizzate le informazioni di base sulla destinazione selezionata.

![barra a destra](../assets/ui/details-page/right-sidebar.png)

La tabella seguente illustra i controlli e i dettagli forniti dalla barra a destra:

| Elemento a barra a destra | Descrizione |
| --- | --- |
| [!UICONTROL Attivare i segmenti] | Seleziona questo controllo per modificare i segmenti mappati alla destinazione, aggiornare le pianificazioni di esportazione o aggiungere e rimuovere attributi e identità mappati. Consulta le guide su [attivazione dei dati sul pubblico per segmentare le destinazioni di streaming](./activate-segment-streaming-destinations.md), [attivazione dei dati sul pubblico in destinazioni basate su profili in batch](./activate-batch-profile-destinations.md)e [attivazione dei dati sul pubblico in streaming su destinazioni basate su profili](./activate-streaming-profile-destinations.md) per ulteriori informazioni. |
| [!UICONTROL Elimina] | Consente di eliminare questo flusso di dati e di rimuovere la mappatura dei segmenti precedentemente attivati, se presenti. |
| [!UICONTROL Nome destinazione] | È possibile modificare questo campo per aggiornare il nome della destinazione. |
| [!UICONTROL Descrizione] | È possibile modificare questo campo per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destinazione] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Consulta la sezione [catalogo delle destinazioni](../catalog/overview.md) per ulteriori informazioni. |
| [!UICONTROL Stato] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Azioni di marketing] | Indica le azioni di marketing (casi d’uso) applicabili a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Categoria] | Indica il tipo di destinazione. Consulta la sezione [catalogo delle destinazioni](../catalog/overview.md) per ulteriori informazioni. |
| [!UICONTROL Tipo di connessione] | Indica il modulo in base al quale i tipi di pubblico vengono inviati alla destinazione. Eventuali valori includono [!UICONTROL Cookie] e [!UICONTROL Basato su profilo]. |
| [!UICONTROL Frequenza] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. Eventuali valori includono [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identità] | Rappresenta lo spazio dei nomi identità accettato dalla destinazione, ad esempio `GAID`, `IDFA`oppure `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, consulta la sezione [panoramica dello spazio dei nomi identità](../../identity-service/namespaces.md). |
| [!UICONTROL Creato da] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Creato] | Indica la data/ora UTC al momento della creazione della destinazione. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Abilitato]/[!UICONTROL Disabilitato] interruttore {#enabled-disabled-toggle}

È possibile utilizzare **[!UICONTROL Abilitato]/[!UICONTROL Disabilitato]** per avviare e mettere in pausa tutte le esportazioni di dati verso la destinazione.

![Attiva o disattiva l&#39;interruttore del flusso di dati](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Corse del flusso di dati] {#dataflow-runs}

La [!UICONTROL Corse del flusso di dati] La scheda fornisce i dati metriche sulle esecuzioni del flusso di dati sulle destinazioni batch e in streaming. Fai riferimento a [Monitorare i flussi di dati](monitor-dataflows.md) per dettagli e definizioni metriche.

>[!NOTE]
>
>* La funzionalità di monitoraggio delle destinazioni è attualmente supportata per tutte le destinazioni in Experience Platform *eccetto* la [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Personalizzazione personalizzata](/help/destinations/catalog/personalization/custom-personalization.md) e [Tipi di pubblico di Experience Cloud](/help/destinations/catalog/adobe/experience-cloud-audiences.md) destinazioni.
>* Per [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Hub eventi di Azure](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)e [API HTTP](/help/destinations/catalog/streaming/http-destination.md) Le destinazioni, le identità escluse, non riuscite e attivate al momento non vengono visualizzate.


![Vista delle esecuzioni del flusso di dati](../assets/ui/details-page/dataflow-runs.png)

### Il flusso di dati esegue la durata {#dataflow-runs-duration}

Esiste un problema noto nella durata di esecuzione del flusso di dati visualizzato. Mentre il **[!UICONTROL Durata dell&#39;elaborazione]** per la maggior parte delle esecuzioni dei flussi di dati sono indicate circa quattro ore, come mostrato nell&#39;immagine seguente, il tempo di elaborazione effettivo per qualsiasi esecuzione dei flussi di dati è molto più breve. Le finestre di esecuzione del flusso di dati rimangono aperte più a lungo nel caso in cui Experience Platform debba riprovare a effettuare chiamate alla destinazione.

![L’immagine del flusso di dati esegue la pagina con la colonna Ora di elaborazione evidenziata.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run.png)

## [!UICONTROL Dati di attivazione] {#activation-data}

La [!UICONTROL Dati di attivazione] visualizza un elenco dei segmenti mappati alla destinazione, con la relativa data di inizio e la data di fine (se applicabile), e altre informazioni rilevanti per l’esportazione dei dati, ad esempio tipo di esportazione, pianificazione e frequenza. Per visualizzare i dettagli di un particolare segmento, selezionane il nome dall’elenco.

>[!TIP]
>
>Per visualizzare e modificare i dettagli relativi agli attributi e alle identità mappati a una destinazione, seleziona **[!UICONTROL Attivare i segmenti]** in [barra a destra](#right-rail).

![Destinazione batch visualizzazione dati attivazione](../assets/ui/details-page/activation-data-batch.png)

![Destinazione streaming visualizzazione dati attivazione](../assets/ui/details-page/activation-data-streaming.png)

>[!NOTE]
>
>Per informazioni dettagliate sull’esplorazione della pagina dei dettagli di un segmento, consulta [Panoramica dell’interfaccia utente di segmentazione](../../segmentation/ui/overview.md#segment-details).
