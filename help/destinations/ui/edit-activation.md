---
keywords: modifica attivazione, modifica destinazione, modifica destinazione
title: Modifica flussi di dati di attivazione
type: Tutorial
description: Segui i passaggi descritti in questo articolo per modificare un flusso di dati di attivazione esistente in Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Modifica flussi di dati di attivazione {#edit-activation-flows}

In Adobe Experience Platform, puoi modificare vari componenti dei flussi di dati di attivazione esistenti nelle destinazioni, come i tipi di pubblico e gli attributi di profilo esportati, la frequenza di esportazione, se il flusso di dati di attivazione è abilitato o disabilitato e altro ancora.

## Modifica flussi di dati {#edit-dataflows}

Per modificare i flussi di dati di attivazione esistenti, effettua le seguenti operazioni:

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Sfoglia]** dall’intestazione in alto per visualizzare i flussi di dati di destinazione esistenti.

   ![Sfoglia destinazioni](../assets/ui/edit-activation/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona filtro](../assets/ui/edit-activation/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/edit-activation/filter-destinations.png)

3. Seleziona il nome del flusso di dati di destinazione da modificare.

   ![Seleziona destinazione](../assets/ui/edit-activation/destination-select.png)

4. Il **[!UICONTROL Il flusso di dati viene eseguito]** viene visualizzata la pagina relativa alla destinazione, con i controlli disponibili. A questo punto, puoi modificare diversi componenti del flusso di dati di destinazione:

   * Seleziona **[!UICONTROL Attiva tipi di pubblico]** nella barra a destra per modificare i tipi di pubblico o gli attributi del profilo da inviare alla destinazione. Questa azione ti porta al flusso di lavoro di attivazione, che varia a seconda del tipo di destinazione. Per ulteriori informazioni, consulta le guide su:
      * [attivazione dei dati sul pubblico nelle destinazioni di streaming del pubblico](./activate-segment-streaming-destinations.md) (ad esempio, Facebook o Twitter);
      * [attivazione dei dati sul pubblico in destinazioni basate su profili batch](./activate-batch-profile-destinations.md) (ad esempio, Amazon S3 o Oracle Eloqua);
      * [attivazione dei dati sul pubblico per lo streaming di destinazioni basate su profili](./activate-streaming-profile-destinations.md) (ad esempio, API HTTP o Amazon Kinesis).

   * Inoltre, puoi modificare il nome e la descrizione del flusso di dati di destinazione.
   * È possibile utilizzare **[!UICONTROL Abilitato]/[!UICONTROL Disabilitato]** attiva per avviare e mettere in pausa tutte le esportazioni di dati nella destinazione.

   ![Dettagli della destinazione](../assets/ui/edit-activation/destination-details.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai utilizzato correttamente il **[!UICONTROL destinazioni]** per aggiornare i flussi di dati di destinazione esistenti.

Per ulteriori informazioni sulle destinazioni, consulta [panoramica sulle destinazioni](../catalog/overview.md).
