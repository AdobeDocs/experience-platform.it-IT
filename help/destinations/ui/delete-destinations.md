---
keywords: eliminare le destinazioni, eliminare le destinazioni
title: Eliminare le destinazioni
type: Tutorial
description: Questa esercitazione elenca i passaggi per eliminare una destinazione esistente nell'interfaccia utente di Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Eliminare le destinazioni {#delete-destinations}

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform puoi eliminare le connessioni esistenti alle destinazioni.

L&#39;eliminazione di una destinazione rimuove tutti i flussi di dati esistenti a tale destinazione. Tutti i segmenti attivati nelle destinazioni eliminate vengono demappati prima che il flusso di dati venga eliminato.

Esistono due modi per eliminare le destinazioni dal [!DNL Platform] [!DNL UI]. È possibile:

* [Elimina le destinazioni dal [!UICONTROL Sfoglia] scheda](#delete-browse-tab)
* [Elimina le destinazioni dalla pagina dei dettagli della destinazione](#delete-destination-details-page)

## Eliminare le destinazioni dalla scheda Sfoglia{#delete-browse-tab}

Segui i passaggi seguenti per eliminare una destinazione dal [!UICONTROL Sfoglia] scheda .

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall’intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleziona la ![Pulsante Altro](../assets/ui/delete-destinations/more-icon.png) nella colonna Nome e selezionare ![Pulsante Elimina](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Elimina]** per rimuovere una connessione di destinazione esistente.
   ![Eliminare le destinazioni](../assets/ui/delete-destinations/delete-destinations.png)

4. Seleziona **[!UICONTROL Elimina]** per confermare la rimozione della connessione di destinazione.

   ![Conferma eliminazione destinazione](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Elimina le destinazioni dalla pagina dei dettagli della destinazione{#delete-destination-details-page}

Segui i passaggi riportati di seguito per eliminare una destinazione dalla pagina dei dettagli della destinazione.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall’intestazione superiore.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtrare le destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Selezionare il nome della destinazione che si desidera eliminare.

   ![Seleziona destinazione](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se la destinazione dispone di flussi di dati esistenti, viene visualizzata la [!UICONTROL Corse del flusso di dati] scheda .

      ![Scheda esecuzioni flusso di dati](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se nella destinazione non sono presenti flussi di dati, vieni portato a una pagina vuota in cui puoi iniziare a attivare i tipi di pubblico.

      ![Dettagli della destinazione](../assets/ui/delete-destinations/destination-details-empty.png)

4. Seleziona **[!UICONTROL Elimina]** nella barra a destra.

   ![Elimina destinazione](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Seleziona **[!UICONTROL Elimina]** nella finestra di dialogo di conferma per rimuovere la destinazione.

   ![Elimina conferma di destinazione](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >A seconda del carico del server, può richiedere alcuni minuti [!DNL Platform] per eliminare la destinazione.
