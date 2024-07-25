---
keywords: eliminare le destinazioni, come eliminare le destinazioni, come eliminare la destinazione
title: Elimina destinazioni
type: Tutorial
description: Questa esercitazione elenca i passaggi per eliminare una destinazione esistente nell'interfaccia utente di Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Elimina destinazioni {#delete-destinations}

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform, puoi eliminare le connessioni esistenti alle destinazioni.

L’eliminazione di una destinazione rimuove tutti i flussi di dati esistenti in tale destinazione. Tutti i tipi di pubblico attivati nelle destinazioni eliminate vengono annullati prima dell’eliminazione del flusso di dati.

Esistono due modi per eliminare le destinazioni da [!DNL Platform] [!DNL UI]. Puoi eseguire le seguenti operazioni:

* [Elimina destinazioni dalla scheda [!UICONTROL Sfoglia]](#delete-browse-tab)
* [Eliminare le destinazioni dalla pagina dei dettagli della destinazione](#delete-destination-details-page)

## Eliminare le destinazioni dalla scheda Sfoglia{#delete-browse-tab}

Segui i passaggi seguenti per eliminare una destinazione dalla scheda [!UICONTROL Sfoglia].

1. Accedi a [interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Selezionare il pulsante ![Altro pulsante](/help/images/icons/more.png) nella colonna Nome, quindi selezionare ![Elimina pulsante](/help/images/icons/delete.png) **[!UICONTROL Elimina]** per rimuovere una connessione di destinazione esistente.
   ![Elimina destinazioni](../assets/ui/delete-destinations/delete-destinations.png)

4. Selezionare **[!UICONTROL Elimina]** per confermare la rimozione della connessione di destinazione.

   ![Conferma eliminazione destinazione](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Eliminare le destinazioni dalla pagina dei dettagli della destinazione{#delete-destination-details-page}

Per eliminare una destinazione dalla pagina dei dettagli della destinazione, segui la procedura riportata di seguito.

1. Accedi a [interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall&#39;intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleziona il nome della destinazione da eliminare.

   ![Seleziona destinazione](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se la destinazione dispone di flussi di dati esistenti, viene visualizzata la scheda [!UICONTROL Esecuzioni flusso di dati].

     ![Il flusso di dati esegue la scheda](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se la destinazione non dispone di flussi di dati esistenti, viene visualizzata una pagina vuota in cui puoi iniziare ad attivare i tipi di pubblico.

     ![Dettagli destinazione](../assets/ui/delete-destinations/destination-details-empty.png)

4. Seleziona **[!UICONTROL Elimina]** nella barra a destra.

   ![Elimina destinazione](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Seleziona **[!UICONTROL Elimina]** nella finestra di dialogo di conferma per rimuovere la destinazione.

   ![Elimina conferma destinazione](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >A seconda del carico del server, l&#39;eliminazione della destinazione può richiedere alcuni minuti per [!DNL Platform].
