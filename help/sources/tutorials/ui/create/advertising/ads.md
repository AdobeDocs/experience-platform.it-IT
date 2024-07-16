---
title: Creare una connessione Source di Google Ads nell’interfaccia utente
description: Scopri come creare una connessione sorgente di Google Ads utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# Creare una connessione sorgente Google Ads nell’interfaccia utente

>[!WARNING]
>
>Origine [!DNL Google Ads] temporaneamente non disponibile. Adobe sta lavorando per risolvere i problemi con questa origine.

>[!NOTE]
>
>Il codice sorgente di Google Ads è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere [Panoramica origini](../../../../home.md#terms-and-conditions).

Questo tutorial descrive i passaggi necessari per creare una connessione sorgente di Google Ads tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione Google Ads valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/advertising.md)

### Raccogli le credenziali richieste

Per accedere alla piattaforma del tuo account Google Ads, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID cliente del client | L’ID cliente client è il numero di account che corrisponde all’account client di Google Ads che desideri gestire con l’API di Google Ads. Questo ID segue il modello di `123-456-7890`. |
| ID cliente accesso | L’ID cliente di accesso è il numero di account che corrisponde all’account di Google Ads Manager e viene utilizzato per recuperare i dati del rapporto da un cliente operativo specifico. Per ulteriori informazioni sull&#39;ID cliente di accesso, leggere la [documentazione API di Google Ads](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Token sviluppatore | Il token sviluppatore ti consente di accedere all’API di Google Ads. Puoi utilizzare lo stesso token sviluppatore per effettuare richieste su tutti gli account Google Ads. Recupera il token di sviluppo [accedendo al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi accedendo alla pagina del Centro API. |
| Aggiorna token | Il token di aggiornamento fa parte dell&#39;autenticazione [!DNL OAuth2]. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| ID client | L&#39;ID client viene utilizzato insieme al segreto client come parte dell&#39;autenticazione [!DNL OAuth2]. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |
| Segreto client | Il segreto client viene utilizzato insieme all&#39;ID client come parte dell&#39;autenticazione [!DNL OAuth2]. Insieme, l’ID client e il segreto client consentono all’applicazione di funzionare per conto dell’account identificando l’applicazione in Google. |

Per ulteriori informazioni su come iniziare a utilizzare Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview), consulta il documento di panoramica sulle API[.

## Connetti il tuo account Google Ads

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Advertising]** selezionare **[!UICONTROL Google Ads]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo origini nell&#39;interfaccia utente Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

Viene visualizzata la pagina **[!UICONTROL Connetti a Google Ads]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per connettere un account esistente, seleziona l&#39;account Google Ads con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![Pagina di selezione per gli account esistenti nel flusso di lavoro di origine.](../../../../images/tutorials/create/ads/existing.png).

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali di Google Ads. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account nel flusso di lavoro di origine.](../../../../images/tutorials/create/ads/new.png).

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Google Ads. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati pubblicitari in Platform](../../dataflow/advertising.md).
