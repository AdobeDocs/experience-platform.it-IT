---
keywords: eliminare le destinazioni, come eliminare le destinazioni, come eliminare la destinazione
title: Elimina destinazioni
type: Tutorial
description: Questa esercitazione elenca i passaggi per eliminare una destinazione esistente nell'interfaccia utente di Adobe Experience Platform
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Elimina destinazioni {#delete-destinations}

## Panoramica {#overview}

Nell’interfaccia utente di Adobe Experience Platform, puoi eliminare le connessioni esistenti alle destinazioni.

L’eliminazione di una destinazione rimuove tutti i flussi di dati esistenti in tale destinazione. Tutti i tipi di pubblico attivati nelle destinazioni eliminate vengono annullati prima dell’eliminazione del flusso di dati.

Esistono due modi per eliminare le destinazioni dal [!DNL Platform] [!DNL UI]. Puoi eseguire le seguenti operazioni:

* [Eliminare le destinazioni dalla [!UICONTROL Sfoglia] scheda](#delete-browse-tab)
* [Eliminare le destinazioni dalla pagina dei dettagli della destinazione](#delete-destination-details-page)

## Eliminare le destinazioni dalla scheda Sfoglia{#delete-browse-tab}

Per eliminare una destinazione dal menu, effettua le seguenti operazioni [!UICONTROL Sfoglia] scheda.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall’intestazione in alto.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleziona la ![Pulsante Altro](../assets/ui/delete-destinations/more-icon.png) nella colonna Nome, quindi selezionare ![Pulsante Elimina](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Elimina]** per rimuovere una connessione di destinazione esistente.
   ![Elimina destinazioni](../assets/ui/delete-destinations/delete-destinations.png)

4. Seleziona **[!UICONTROL Elimina]** per confermare la rimozione della connessione di destinazione.

   ![Conferma eliminazione destinazione](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Eliminare le destinazioni dalla pagina dei dettagli della destinazione{#delete-destination-details-page}

Per eliminare una destinazione dalla pagina dei dettagli della destinazione, segui la procedura riportata di seguito.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Per visualizzare le destinazioni esistenti, seleziona **[!UICONTROL Sfoglia]** dall’intestazione in alto.

   ![Sfoglia destinazioni](../assets/ui/delete-destinations/browse-destinations.png)

2. Seleziona l’icona del filtro ![Icona filtro](../assets/ui/delete-destinations/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di flussi di dati associati alla destinazione selezionata.

   ![Filtra destinazioni](../assets/ui/delete-destinations/filter-destinations.png)

3. Seleziona il nome della destinazione da eliminare.

   ![Seleziona destinazione](../assets/ui/delete-destinations/delete-destination-select.png)

   * Se la destinazione dispone di flussi di dati esistenti, viene visualizzato il [!UICONTROL Il flusso di dati viene eseguito] scheda.

     ![Scheda Esecuzioni flusso di dati](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Se la destinazione non dispone di flussi di dati esistenti, viene visualizzata una pagina vuota in cui puoi iniziare ad attivare i tipi di pubblico.

     ![Dettagli della destinazione](../assets/ui/delete-destinations/destination-details-empty.png)

4. Seleziona **[!UICONTROL Elimina]** nella barra a destra.

   ![Elimina destinazione](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Seleziona **[!UICONTROL Elimina]** nella finestra di dialogo di conferma per rimuovere la destinazione.

   ![Conferma eliminazione destinazione](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >A seconda del carico del server, potrebbero essere necessari alcuni minuti per [!DNL Platform] per eliminare la destinazione.
