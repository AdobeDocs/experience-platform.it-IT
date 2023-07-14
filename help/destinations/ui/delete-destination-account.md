---
keywords: eliminare l'account di destinazione, gli account di destinazione, come eliminare gli account
title: Elimina account di destinazione
type: Tutorial
description: Questo tutorial elenca i passaggi per eliminare gli account di destinazione nell’interfaccia utente di Adobe Experience Platform
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Elimina account di destinazione

## Panoramica {#overview}

Il **[!UICONTROL Account]** Questa scheda mostra i dettagli sulle connessioni stabilite con varie destinazioni. Consulta la sezione [Panoramica sugli account](../ui/destinations-workspace.md#accounts) per tutte le informazioni che puoi ottenere su ciascun account di destinazione.

Questo tutorial illustra i passaggi necessari per eliminare gli account di destinazione che non sono più necessari utilizzando l’interfaccia utente di Experience Platform.

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

## Elimina account {#delete}

>[!TIP]
>
>Prima di eliminare l’account di destinazione, devi eliminare tutti i flussi di dati esistenti associati all’account di destinazione. Per eliminare i flussi di dati di destinazione esistenti, consulta l’esercitazione su [eliminazione dei flussi di dati di destinazione nell’interfaccia utente](./delete-destinations.md).

Per eliminare gli account di destinazione esistenti, effettua le seguenti operazioni.

1. Accedi a [Interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Account]** nell’intestazione in alto per visualizzare i tuoi account esistenti.

   ![Scheda Account](../assets/ui/delete-accounts/accounts-tab.png)

2. Seleziona l’icona del filtro ![Icona filtro](../assets/ui/update-accounts/filter.png) in alto a sinistra per avviare il pannello ordina. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtra destinazioni](../assets/ui/delete-accounts/filter-accounts.png)

3. Seleziona i puntini di sospensione (`...`) accanto al nome dell&#39;account che si desidera eliminare. Viene visualizzato un pannello a comparsa che fornisce le opzioni per **[!UICONTROL Attiva tipi di pubblico]**, **[!UICONTROL Modifica dettagli]**, e **[!UICONTROL Elimina]** l’account. Seleziona la ![Pulsante Elimina](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Elimina]** per eliminare l’account desiderato.

   ![Elimina account di destinazione](../assets/ui/delete-accounts/delete-accounts.png)

4. Viene visualizzata una finestra di dialogo di conferma finale, seleziona **[!UICONTROL Elimina]** per completare il processo.

![Conferma eliminazione account](../assets/ui/delete-accounts/confirm-account-deletion.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro delle destinazioni per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando [!DNL Flow Service] API, fai riferimento al tutorial su [eliminazione di connessioni tramite l’API del servizio Flusso](../api/delete-destination-account.md)
