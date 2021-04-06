---
keywords: destinazioni;destinazione;pagina dettagli destinazioni;pagina dettagli destinazioni
title: Visualizza dettagli destinazione
description: 'La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati. '
seo-description: La pagina dei dettagli di una singola destinazione fornisce una panoramica dei dettagli della destinazione. I dettagli della destinazione includono il nome della destinazione, l’ID, i segmenti mappati alla destinazione e i controlli per modificare l’attivazione e per abilitare e disabilitare il flusso di dati.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Visualizza dettagli destinazione

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e monitorare gli attributi e le attività delle destinazioni. Questi dettagli includono il nome e l’ID della destinazione, i controlli per attivare o disattivare le destinazioni e altro ancora. I dettagli per le destinazioni batch includono anche metriche per i record di profilo attivati e una cronologia delle esecuzioni dei flussi di dati.

>[!NOTE]
>
>La pagina dei dettagli delle destinazioni fa parte dell’area di lavoro [!UICONTROL Destinations] in [!DNL Platform] [!DNL UI]. Per ulteriori informazioni, consulta la [[!UICONTROL Destinations] panoramica dell&#39;area di lavoro](./destinations-workspace.md) .

## Visualizza i dettagli di destinazione {#view-details}

Segui i passaggi riportati di seguito per visualizzare ulteriori dettagli su una destinazione esistente.

1. Accedi a [Interfaccia Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Browse]** dall’intestazione superiore per visualizzare le destinazioni esistenti.

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
| [!UICONTROL Activate] | Seleziona questo controllo per modificare i segmenti mappati alla destinazione. Per ulteriori informazioni, consulta la guida sull’ [attivazione dei segmenti su una destinazione](./activate-destinations.md) . |
| [!UICONTROL Delete] | Consente di eliminare questo flusso di dati e di rimuovere la mappatura dei segmenti precedentemente attivati, se presenti. |
| [!UICONTROL Destination name] | È possibile modificare questo campo per aggiornare il nome della destinazione. |
| [!UICONTROL Description] | È possibile modificare questo campo per aggiornare o aggiungere una descrizione facoltativa alla destinazione. |
| [!UICONTROL Destination] | Rappresenta la piattaforma di destinazione a cui vengono inviati i tipi di pubblico. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Status] | Indica se la destinazione è abilitata o disabilitata. |
| [!UICONTROL Marketing actions] | Indica le azioni di marketing (casi d’uso) applicabili a questa destinazione a scopo di governance dei dati. |
| [!UICONTROL Category] | Indica il tipo di destinazione. Per ulteriori informazioni, consulta il [catalogo delle destinazioni](../catalog/overview.md) . |
| [!UICONTROL Connection type] | Indica il modulo in base al quale i tipi di pubblico vengono inviati alla destinazione. I valori possibili sono [!UICONTROL Cookie] e [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Indica la frequenza con cui i tipi di pubblico vengono inviati alla destinazione. I valori possibili sono [!UICONTROL Streaming] e [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Rappresenta lo spazio dei nomi di identità accettato dalla destinazione, ad esempio `GAID`, `IDFA` o `email`. Per ulteriori informazioni sugli spazi dei nomi di identità accettati, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md). |
| [!UICONTROL Created by] | Indica l&#39;utente che ha creato la destinazione. |
| [!UICONTROL Created] | Indica la data/ora UTC al momento della creazione della destinazione. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

Puoi utilizzare l’interruttore **[!UICONTROL Enabled]/[!UICONTROL Disabled]** per avviare e mettere in pausa tutte le esportazioni di dati verso la destinazione.

![Attiva/disattiva attivazione/disattivazione](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

La scheda [!UICONTROL Dataflow runs] fornisce dati metrici sul flusso di dati da eseguire su destinazioni batch. Per ulteriori informazioni, fare riferimento a [Flussi dati di monitoraggio](monitor-dataflows.md).

## [!UICONTROL Activation data] {#activation-data}

La scheda [!UICONTROL Activation data] visualizza un elenco di segmenti mappati sulla destinazione, con le relative date di inizio e di fine (se applicabili). Per visualizzare i dettagli di un particolare segmento, selezionane il nome dall’elenco.

![Dati di attivazione](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;esplorazione della pagina dei dettagli di un segmento, consulta la [Panoramica dell&#39;interfaccia utente di segmentazione](../../segmentation/ui/overview.md#segment-details).
