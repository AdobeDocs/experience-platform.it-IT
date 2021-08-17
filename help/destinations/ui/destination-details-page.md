---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni
title: Visualizza dettagli destinazione
description: 'La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati. '
seo-description: La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# Visualizza dettagli destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli per le destinazioni batch includono anche metriche per i record di profilo attivati e una cronologia delle esecuzioni dei flussi di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte dell’area di lavoro [!UICONTROL Destinazioni] in [!DNL Platform] [!DNL UI]. Per ulteriori informazioni, consulta la [[!UICONTROL Panoramica dell’area di lavoro ] Destinazioni](./destinations-workspace.md) .

## Visualizza dettagli destinazione {#view-details}

Segui i passaggi riportati di seguito per visualizzare ulteriori dettagli su una destinazione esistente.

1. Accedi a [Interfaccia Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore per visualizzare le destinazioni esistenti.

   ![Sfoglia destinazioni](../assets/ui/details-page/browse-destinations.png)

1. Seleziona l&#39;icona del filtro ![Icona-filtro](../assets/ui/details-page/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/details-page/filter-destinations.png)

1. Selezionare il nome della destinazione che si desidera visualizzare.

   ![Seleziona destinazione](../assets/ui/details-page/destination-select.png)

1. Viene visualizzata la pagina dei dettagli della destinazione, con i relativi controlli disponibili. Se visualizzi i dettagli di una destinazione batch, viene visualizzata anche una dashboard di monitoraggio.

   ![Dettagli della destinazione](../assets/ui/details-page/destination-details.png)

## Barra a destra

Nella barra a destra sono visualizzate le informazioni di base sulla destinazione selezionata.

![barra a destra](../assets/ui/details-page/right-sidebar.png)

La tabella seguente illustra i controlli e i dettagli forniti dalla barra a destra:

| Elemento a barra a destra | Descrizione |
| --- | --- |
| [!UICONTROL Attiva] | Seleziona questo controllo per modificare i segmenti mappati alla destinazione. Per ulteriori informazioni, consulta le guide sull’ [attivazione dei dati sul pubblico per segmentare le destinazioni di streaming](./activate-segment-streaming-destinations.md), [attivazione dei dati sul pubblico per le destinazioni basate su profili in batch](./activate-batch-profile-destinations.md) e [attivazione dei dati sul pubblico per le destinazioni basate su profili in streaming](./activate-streaming-profile-destinations.md) . |
| [!UICONTROL Elimina] | Consente di eliminare questo flusso di dati e di rimuovere la mappatura dei segmenti precedentemente attivati, se presenti. |
| [!UICONTROL Nome destinazione] | È possibile modificare questo campo per aggiornare il nome della destinazione. |
| [!UICONTROL Descrizione] | È possibile modificare questo campo per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destinazione] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Stato] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Azioni di marketing] | Indica le azioni di marketing (casi d’uso) applicabili a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Categoria] | Indica il tipo di destinazione. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Tipo di connessione] | Indica il modulo in base al quale i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Cookie] e [!UICONTROL basati su profilo]. |
| [!UICONTROL Frequenza] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. I valori possibili includono [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identità] | Rappresenta lo spazio dei nomi di identità accettato dalla destinazione, ad esempio `GAID`, `IDFA` o `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md). |
| [!UICONTROL Creato da] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Creato] | Indica la data/ora UTC al momento della creazione della destinazione. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Attivato]/ Disattivato/Disattivato

Puoi utilizzare l&#39;interruttore **[!UICONTROL Enabled]/[!UICONTROL Disabled]** per avviare e mettere in pausa tutte le esportazioni di dati verso la destinazione.

![Attiva/disattiva attivazione/disattivazione](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Corse del flusso di dati]

La scheda [!UICONTROL Flusso di dati esegue] fornisce i dati della metrica nel flusso di dati che vengono eseguiti su destinazioni batch. Per ulteriori informazioni, fare riferimento a [Flussi dati di monitoraggio](monitor-dataflows.md).

## [!UICONTROL Dati di attivazione] {#activation-data}

La scheda [!UICONTROL Dati di attivazione] visualizza un elenco di segmenti mappati alla destinazione, con le relative date di inizio e di fine (se applicabili). Per visualizzare i dettagli di un particolare segmento, selezionane il nome dall’elenco.

![Dati di attivazione](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;esplorazione della pagina dei dettagli di un segmento, consulta la [Panoramica dell&#39;interfaccia utente di segmentazione](../../segmentation/ui/overview.md#segment-details).
