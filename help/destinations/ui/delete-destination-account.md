---
keywords: eliminare l'account di destinazione, gli account di destinazione, come eliminare gli account
title: Elimina account di destinazione
type: Tutorial
description: Questo tutorial elenca i passaggi per eliminare gli account di destinazione nell’interfaccia utente di Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Elimina account di destinazione

## Panoramica {#overview}

La scheda **[!UICONTROL Account]** mostra i dettagli sulle connessioni stabilite con varie destinazioni. Per tutte le informazioni che puoi ottenere su ciascun account di destinazione, consulta la [Panoramica account](../ui/destinations-workspace.md#accounts).

Questo tutorial illustra i passaggi necessari per eliminare gli account di destinazione che non sono più necessari utilizzando l’interfaccia utente di Experience Platform.

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

## Elimina account {#delete}

>[!TIP]
>
>Prima di eliminare l’account di destinazione, devi eliminare tutti i flussi di dati esistenti associati all’account di destinazione. Per eliminare i flussi di dati di destinazione esistenti, fare riferimento all&#39;esercitazione su [eliminazione dei flussi di dati di destinazione nell&#39;interfaccia utente](./delete-destinations.md).

Per eliminare gli account di destinazione esistenti, effettua le seguenti operazioni.

1. Accedi a [interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Account]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

   ![Scheda Account](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtra destinazioni](../assets/ui/delete-accounts/filter-accounts.png)

3. Selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account che si desidera eliminare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL attivare i tipi di pubblico]**, **[!UICONTROL modificare i dettagli]** e **[!UICONTROL eliminare]** l&#39;account. Selezionare il pulsante ![Elimina](/help/images/icons/delete.png) **[!UICONTROL Elimina]** per eliminare l&#39;account desiderato.

   ![Elimina account di destinazione](../assets/ui/delete-accounts/delete-accounts.png)

4. Viene visualizzata una finestra di dialogo di conferma finale. Selezionare **[!UICONTROL Elimina]** per completare il processo.

![Conferma eliminazione account](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro delle destinazioni per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento al tutorial sull&#39;eliminazione di connessioni con l&#39;API del servizio Flusso](../api/delete-destination-account.md)[
