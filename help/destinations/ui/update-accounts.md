---
keywords: aggiornare account di destinazione;account di destinazione;come aggiornare gli account
title: Aggiorna account di destinazione
type: Tutorial
description: Questa esercitazione elenca i passaggi per aggiornare gli account di destinazione nell'interfaccia utente di Adobe Experience Platform
translation-type: tm+mt
source-git-commit: e4afbdd6ff8f45ea8d5506f0228f0a80b44eee51
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 1%

---


# Aggiorna account di destinazione

## Panoramica {#overview}

La scheda **[!UICONTROL Accounts]** mostra i dettagli sulle connessioni stabilite con diverse destinazioni. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ogni destinazione:

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

| Elemento | Descrizione |
|---|---|
| [!UICONTROL Platform] | Destinazione per la quale è stata impostata la connessione. |
| [!UICONTROL Connection Type] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di marketing e-mail: Può essere S3 o FTP.</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server</li><li>Per le destinazioni di archiviazione cloud Amazon S3: Chiave di accesso </li><li>Per le destinazioni di archiviazione cloud SFTP: Autenticazione di base per SFTP</li></ul> |
| [!UICONTROL Username] | Il nome utente selezionato nella [procedura guidata di connessione alla destinazione](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Rappresenta il numero di flussi di destinazione univoci collegati alle informazioni di base create per una destinazione. |
| [!UICONTROL Authorized] | Data di autorizzazione della connessione a questa destinazione. |

## Aggiorna account {#update}

Per aggiornare i dettagli di connessione alle destinazioni esistenti, effettua le seguenti operazioni.

1. Accedi a [Interfaccia Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Accounts]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

   ![Scheda Account](../assets/ui/update-accounts/accounts-tab.png)

2. Seleziona l&#39;icona del filtro ![Icona-filtro](../assets/ui/update-accounts/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello di ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtrare le destinazioni](../assets/ui/update-accounts/filter-accounts.png)

3. Seleziona il pulsante ![Modifica account](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Edit]** nella colonna **[!UICONTROL Platform]** per modificare le informazioni dell&#39;account.

   ![Scheda Account](../assets/ui/update-accounts/accounts-edit.png)

4. Immetti le credenziali account aggiornate.

   * Per gli account che utilizzano un tipo di connessione `OAuth2`, selezionare **[!UICONTROL Reconnect OAuth]** per rinnovare le credenziali dell&#39;account.

      ![Modifica dettagli OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * Per gli account che utilizzano un tipo di connessione `Access Key` o `ConnectionString`, puoi modificare le informazioni di autenticazione dell’account, incluse informazioni quali ID di accesso, chiavi segrete o stringhe di connessione.

      ![Modifica dettagli Chiave di accesso](../assets/ui/update-accounts/edit-details-key.png)

5. Selezionare **[!UICONTROL Save]** per completare l&#39;aggiornamento delle credenziali.
