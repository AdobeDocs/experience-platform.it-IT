---
keywords: eliminare l'account di destinazione, gli account di destinazione, come eliminare gli account
title: Elimina account di destinazione
type: Tutorial
description: Questo tutorial elenca i passaggi per eliminare gli account di destinazione nell’interfaccia utente di Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%

---

# Elimina account di destinazione

## Panoramica {#overview}

La scheda **[!UICONTROL Accounts]** mostra i dettagli sulle connessioni stabilite con varie destinazioni. Per tutte le informazioni disponibili per ciascun account di destinazione, vedere [Panoramica account](../ui/destinations-workspace.md#accounts).

Questo tutorial illustra i passaggi necessari per eliminare gli account di destinazione non più necessari tramite l’interfaccia utente di Experience Platform.

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

## Elimina account {#delete}

>[!TIP]
>
>Prima di eliminare l’account di destinazione, devi eliminare tutti i flussi di dati esistenti associati all’account di destinazione. Per eliminare i flussi di dati di destinazione esistenti, fare riferimento all&#39;esercitazione su [eliminazione dei flussi di dati di destinazione nell&#39;interfaccia utente](./delete-destinations.md).

Per eliminare gli account di destinazione esistenti, effettua le seguenti operazioni.

1. Vai alla [interfaccia utente di Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Accounts]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

   ![Scheda Account](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtra destinazioni](../assets/ui/delete-accounts/filter-accounts.png)

3. Selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account che si desidera eliminare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL Activate audiences]**, **[!UICONTROL Edit details]** e **[!UICONTROL Delete]** l&#39;account. Selezionare il pulsante ![Elimina](/help/images/icons/delete.png) **[!UICONTROL Delete]** per eliminare l&#39;account desiderato.

   ![Elimina account di destinazione](../assets/ui/delete-accounts/delete-accounts.png)

4. Viene visualizzata una finestra di dialogo di conferma finale. Selezionare **[!UICONTROL Delete]** per completare il processo.

![Conferma eliminazione account](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Passaggi successivi {#next-steps}

Hai utilizzato correttamente l’area di lavoro delle destinazioni per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento al tutorial sull&#39;eliminazione di connessioni mediante l&#39;API del servizio Flusso[&#128279;](../api/delete-destination-account.md)
