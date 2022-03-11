---
keywords: modificare l'attivazione, modificare la destinazione, modificare la destinazione
title: Modificare i flussi di dati di attivazione
type: Tutorial
seo-title: Edit activation dataflows
description: Segui i passaggi descritti in questo articolo per modificare un flusso di dati di attivazione esistente in Adobe Experience Platform.
seo-description: Follow the steps in this article to edit an existing activation dataflow in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 2d944c7bd237efbbd4a770b3a6dd03c4133bc901
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Modificare i flussi di dati di attivazione {#edit-activation-flows}

In Adobe Experience Platform, puoi modificare vari componenti dei flussi di dati di attivazione esistenti nelle destinazioni, come i segmenti esportati e gli attributi di profilo, la frequenza di esportazione, se il flusso di dati di attivazione è abilitato o disabilitato e altro ancora.

Per modificare i flussi di dati di attivazione esistenti, effettua le seguenti operazioni:

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione superiore per visualizzare i flussi di dati di destinazione esistenti.

   ![Sfoglia destinazioni](../assets/ui/edit-activation/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/edit-activation/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/edit-activation/filter-destinations.png)

3. Seleziona il nome del flusso di dati di destinazione da modificare.

   ![Seleziona destinazione](../assets/ui/edit-activation/destination-select.png)

4. La **[!UICONTROL Corse del flusso di dati]** viene visualizzata la pagina della destinazione, con i relativi controlli disponibili. A questo punto, puoi modificare diversi componenti del flusso di dati di destinazione:

   * Seleziona **[!UICONTROL Attivare i segmenti]** nella barra a destra per modificare i segmenti o gli attributi di profilo da inviare alla destinazione. Questa azione ti porta al flusso di lavoro di attivazione, che varia a seconda del tipo di destinazione. Per ulteriori informazioni, consulta le guide su:
      * [attivazione dei dati sul pubblico per segmentare le destinazioni di streaming](./activate-segment-streaming-destinations.md) (ad esempio, Facebook o Twitter);
      * [attivazione dei dati sul pubblico in destinazioni basate su profili in batch](./activate-batch-profile-destinations.md) (ad esempio, Amazon S3 o Oracle Eloqua);
      * [attivazione dei dati sul pubblico in streaming su destinazioni basate su profili](./activate-streaming-profile-destinations.md) (ad esempio, HTTP API o Amazon Kinesis).
   * Inoltre, puoi modificare il nome e la descrizione del flusso di dati di destinazione.
   * È possibile utilizzare **[!UICONTROL Abilitato]/[!UICONTROL Disabilitato]** per avviare e mettere in pausa tutte le esportazioni di dati verso la destinazione.

   ![Dettagli della destinazione](../assets/ui/edit-activation/destination-details.png)

5. Fai riferimento a [Panoramica sull’attivazione](activation-overview.md) per informazioni su come attivare nuovi segmenti nelle destinazioni.
