---
keywords: Experience Platform;home;argomenti popolari;Google Ads;connettore di origine Google Ads;connettore google ads
title: Creare una connessione sorgente di Google Ads nell’interfaccia utente
description: Scopri come creare una connessione sorgente di Google Ads utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 1%

---

# Creare una connessione sorgente Google Ads nell’interfaccia utente

>[!NOTE]
>
>Il codice sorgente di Google Ads è in versione beta. Consulta la [Panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questa esercitazione descrive i passaggi per la creazione di un connettore di origine Google Ads tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione Google Ads valida, puoi saltare il resto del documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/advertising.md)

### Raccogli le credenziali richieste

Per accedere alla piattaforma del tuo account Google Ads, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID cliente client | L’ID cliente client è il numero di account che corrisponde all’account client di Google Ads che desideri gestire con l’API di Google Ads. Questo ID segue il modello di `123-456-7890`. |
| Token sviluppatore | Il token sviluppatore ti consente di accedere all’API di Google Ads. Puoi utilizzare lo stesso token sviluppatore per effettuare richieste su tutti gli account Google Ads. Recupera il token di sviluppo tramite [accesso al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi alla pagina API Center. |
| Aggiorna token | Il token di aggiornamento fa parte di [!DNL OAuth2] autenticazione. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| ID client | L’ID client viene utilizzato insieme al segreto client come parte di [!DNL OAuth2] autenticazione. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |
| Segreto client | Il segreto client viene utilizzato insieme all&#39;ID client come parte [!DNL OAuth2] autenticazione. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |

Leggi il documento di panoramica API per [ulteriori informazioni su come iniziare a utilizzare Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Connetti il tuo account Google Ads

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Pubblicità]** categoria, seleziona **[!UICONTROL Google Ads]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Immagine dell’origine Google Ads nel catalogo delle origini dell’interfaccia utente Experience Platform](../../../../images/tutorials/create/ads/catalog.png).

Il **[!UICONTROL Connetti a Google Ads]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l’account Google Ads con cui desideri connetterti, quindi fai clic su **[!UICONTROL Successivo]** per procedere.

![Immagine di un elenco di account esistenti che puoi utilizzare per creare un flusso di dati Google Ads con](../../../../images/tutorials/create/ads/existing.png).

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali di Google Ads. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![Immagine della schermata di connessione del nuovo account nell’interfaccia utente di Experience Platform](../../../../images/tutorials/create/ads/connect.png).

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Google Ads. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati pubblicitari in Platform](../../dataflow/advertising.md).
