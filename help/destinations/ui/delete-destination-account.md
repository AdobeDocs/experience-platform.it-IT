---
keywords: eliminare account di destinazione, account di destinazione, come eliminare account
title: Elimina account di destinazione
type: Tutorial
description: Questa esercitazione elenca i passaggi per eliminare gli account di destinazione nell'interfaccia utente di Adobe Experience Platform
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Elimina account di destinazione

## Panoramica {#overview}

La **[!UICONTROL Account]** La scheda ti mostra i dettagli sulle connessioni che hai stabilito con diverse destinazioni. Fai riferimento a [Panoramica account](../ui/destinations-workspace.md#accounts) per tutte le informazioni che puoi ottenere su ogni account di destinazione.

Questa esercitazione descrive i passaggi per eliminare gli account di destinazione che non sono più necessari utilizzando l&#39;interfaccia utente di Experience Platform.

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

## Elimina account {#delete}

>[!TIP]
>
>Prima di eliminare l&#39;account di destinazione, è necessario eliminare tutti i flussi di dati esistenti associati all&#39;account di destinazione. Per eliminare i flussi di dati di destinazione esistenti, consulta l’esercitazione su [eliminazione dei flussi di dati di destinazione nell’interfaccia utente](./delete-destinations.md).

Segui i passaggi riportati di seguito per eliminare gli account di destinazione esistenti.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Account]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

   ![Scheda Account](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleziona l’icona del filtro ![Icona Filtro](../assets/ui/update-accounts/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtrare le destinazioni](../assets/ui/delete-accounts/filter-accounts.png)

3. Seleziona i puntini di sospensione (`...`) accanto al nome dell’account da eliminare. Viene visualizzato un pannello a comparsa che fornisce le opzioni per **[!UICONTROL Attivare i segmenti]**, **[!UICONTROL Modifica dettagli]** e **[!UICONTROL Elimina]** il conto. Seleziona la ![Pulsante Elimina](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Elimina]** per eliminare l’account desiderato.

   ![Elimina account di destinazione](../assets/ui/delete-accounts/delete-accounts.png)

4. Viene visualizzata una finestra di dialogo di conferma finale, seleziona **[!UICONTROL Elimina]** per completare il processo.

![Conferma eliminazione account](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro Destinazioni per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando il [!DNL Flow Service] API, consulta l’esercitazione su [eliminazione di connessioni tramite l’API del servizio di flusso](../api/delete-destination-account.md)
