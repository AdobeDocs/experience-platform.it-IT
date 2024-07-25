---
keywords: aggiornare l'account di destinazione, gli account di destinazione, come aggiornare gli account, aggiornare la destinazione
title: Aggiorna account di destinazione
type: Tutorial
description: Questo tutorial elenca i passaggi per aggiornare gli account di destinazione nell’interfaccia utente di Adobe Experience Platform
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Aggiorna account di destinazione

## Panoramica {#overview}

La scheda **[!UICONTROL Account]** mostra i dettagli sulle connessioni stabilite con varie destinazioni. Per tutte le informazioni che puoi ottenere su ciascun account di destinazione, consulta la [Panoramica account](../ui/destinations-workspace.md#accounts).

Questo tutorial illustra i passaggi necessari per aggiornare i dettagli dell’account di destinazione utilizzando l’interfaccia utente di Experience Platform.

Puoi aggiornare i dettagli dell’account di destinazione per aggiornare e autenticare nuovamente le credenziali per gli account correnti o scaduti per le destinazioni attualmente in uso. In genere, i token OAuth e bearer hanno una durata limitata, a seconda della piattaforma di destinazione. Quando questi token scadono, puoi aggiornarli nel flusso di lavoro descritto di seguito. Questo flusso di lavoro ti indirizza a passare attraverso il flusso di lavoro OAuth o a reinserire un token. Analogamente, se nella piattaforma a valle è stata modificata una password o un accesso utente, è possibile aggiornare le credenziali.

Per le destinazioni batch, puoi aggiornare l’accesso o la chiave segreta, se è stata modificata una di queste. Inoltre, se si desidera crittografare i file in futuro, è possibile inserire una chiave pubblica RSA e i file esportati verranno crittografati in futuro.

![Scheda Account](../assets/ui/update-accounts/destination-accounts.png)

## Aggiorna account {#update}

Per aggiornare i dettagli di connessione alle destinazioni esistenti, segui la procedura riportata di seguito.

1. Accedi a [interfaccia utente Experience Platform](https://platform.adobe.com/) e seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra. Seleziona **[!UICONTROL Account]** dall&#39;intestazione superiore per visualizzare gli account esistenti.

   ![Scheda Account](../assets/ui/update-accounts/accounts-tab.png)

2. Seleziona l&#39;icona del filtro ![Icona filtro](/help/images/icons/filter.png) in alto a sinistra per avviare il pannello di ordinamento. Il pannello Ordinamento fornisce un elenco di tutte le destinazioni. Puoi selezionare più di una destinazione dall’elenco per visualizzare una selezione filtrata di account associati alle destinazioni selezionate.

   ![Filtra account di destinazione](../assets/ui/update-accounts/filter-accounts.png)

3. Selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account da aggiornare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL attivare i tipi di pubblico]**, **[!UICONTROL modificare i dettagli]** e **[!UICONTROL eliminare]** l&#39;account. Selezionare il pulsante ![Modifica dettagli](/help/images/icons/edit.png) **[!UICONTROL Modifica dettagli]** per modificare le informazioni sull&#39;account.

   ![Modifica account](../assets/ui/update-accounts/accounts-edit.png)

4. Immetti le credenziali dell&#39;account aggiornate.

   * Per gli account che utilizzano un tipo di connessione `OAuth1` o `OAuth2`, seleziona **[!UICONTROL Riconnetti OAuth]** per rinnovare le credenziali dell&#39;account. Puoi anche aggiornare il nome e la descrizione dell’account.

   ![Modifica dettagli OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * Per gli account che utilizzano un tipo di connessione `Access Key` o `ConnectionString`, è possibile modificare le informazioni di autenticazione dell&#39;account, incluse informazioni quali l&#39;ID di accesso, le chiavi segrete o le stringhe di connessione. Puoi anche aggiornare il nome e la descrizione dell’account.

   ![Modifica dettagli chiave di accesso](../assets/ui/update-accounts/edit-details-key.png)

   * Per gli account che utilizzano un tipo di connessione `Bearer token`, è possibile immettere un nuovo token Bearer, se necessario. Puoi anche aggiornare il nome e la descrizione dell’account.

   ![Modifica token Bearer dei dettagli](../assets/ui/update-accounts/edit-details-bearer.png)

   * Per gli account che utilizzano un tipo di connessione `Server to server`, è possibile aggiornare il nome e la descrizione dell&#39;account.

   ![Modifica dettagli da server a server](../assets/ui/update-accounts/edit-details-s2s.png)

5. Seleziona **[!UICONTROL Salva]** per completare l&#39;aggiornamento dei dettagli account.

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro **[!UICONTROL destinazioni]** per aggiornare gli account esistenti.

Per ulteriori informazioni sulle destinazioni, consulta la [panoramica sulle destinazioni](../catalog/overview.md).