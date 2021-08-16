---
keywords: eliminare le destinazioni, eliminare le destinazioni
title: Eliminare le destinazioni
type: Tutorial
description: Questa esercitazione elenca i passaggi per eliminare una destinazione esistente nell'interfaccia utente di Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 84deb9d1eecee8ec4369915a0b3c1eb810fd7c9b
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Eliminare le destinazioni {#delete-destinations}

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi eliminare le connessioni esistenti alle destinazioni.

L&#39;eliminazione di una destinazione rimuove tutti i flussi di dati esistenti a tale destinazione. Tutti i segmenti attivati nelle destinazioni eliminate vengono demappati prima che il flusso di dati venga eliminato.

Esistono due modi per eliminare le destinazioni dal [!DNL Platform] [!DNL UI] . È possibile:

* [Elimina le destinazioni dalla scheda [!UICONTROL Sfoglia]](#delete-browse-tab)
* [Elimina le destinazioni dalla pagina dei dettagli della destinazione](#delete-destination-details-page)

>[!IMPORTANT]
>
>Anche se è possibile eliminare le *connessioni esistenti alle destinazioni*, come descritto in questo articolo, Platform attualmente non consente di eliminare gli account di destinazione *[esistenti](/help/destinations/ui/destinations-workspace.md#accounts)*.

## Eliminare le destinazioni dalla scheda Sfoglia{#delete-browse-tab}

Segui i passaggi riportati di seguito per eliminare una destinazione dalla scheda [!UICONTROL Sfoglia] .

1. Accedi a [Interfaccia Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona-filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleziona il pulsante ![Elimina](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Elimina]** nella colonna **[!UICONTROL Piattaforma]** per rimuovere una destinazione esistente.
   ![Eliminare le destinazioni](../assets/ui/delete-destinations/delete-destinations.png)

4. Selezionare **[!UICONTROL Elimina]** per confermare la rimozione della destinazione.

   ![Conferma eliminazione destinazione](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Elimina le destinazioni dalla pagina dei dettagli della destinazione{#delete-destination-details-page}

Segui i passaggi riportati di seguito per eliminare una destinazione dalla pagina dei dettagli della destinazione.

1. Accedi a [Interfaccia Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona-filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Selezionare il nome della destinazione che si desidera eliminare.

   ![Seleziona destinazione](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se la destinazione dispone di flussi di dati esistenti, viene visualizzata la scheda [!UICONTROL Il flusso di dati viene eseguito].

      ![Scheda esecuzioni flusso di dati](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se nella destinazione non sono presenti flussi di dati, vieni portato a una pagina vuota in cui puoi iniziare a attivare i tipi di pubblico.

      ![Dettagli della destinazione](../assets/ui/delete-destinations/destination-details-empty.png)


4. Seleziona **[!UICONTROL Elimina]** nella barra a destra.

   ![Elimina destinazione](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Seleziona **[!UICONTROL Elimina]** nella finestra di dialogo di conferma per rimuovere la destinazione.

   ![Elimina conferma di destinazione](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >A seconda del caricamento del server, l’eliminazione della destinazione può richiedere alcuni minuti [!DNL Platform].
