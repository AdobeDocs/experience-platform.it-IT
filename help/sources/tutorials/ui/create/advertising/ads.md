---
title: Creare una connessione sorgente Google Ads nell’interfaccia utente
description: Scopri come creare una connessione sorgente Google Ads utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ac87434c857a39f4be3714cba57519cbb4fa54a6
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Creare una connessione sorgente Google Ads nell’interfaccia utente

>[!NOTE]
>
>L&#39;origine Google Ads è in versione beta. Consulta la sezione [Panoramica delle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente Google Ads utilizzando l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei seguenti componenti dell&#39;Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione Google Ads valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/advertising.md)

### Raccogli credenziali richieste

Per accedere alla piattaforma account Google Ads, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID cliente client | L’ID cliente client è il numero di account che corrisponde all’account client Google Ads che desideri gestire con l’API Google Ads. Questo ID segue il modello di `123-456-7890`. |
| ID cliente di accesso | L’ID cliente di accesso è il numero di account che corrisponde al tuo account Google Ads manager e viene utilizzato per recuperare i dati del rapporto da un cliente operativo specifico. Per ulteriori informazioni sull&#39;ID cliente di accesso, consulta la sezione [Documentazione API di Google Ads](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| Token per sviluppatori | Il token sviluppatore ti consente di accedere all’API Google Ads. Puoi usare lo stesso token sviluppatore per effettuare richieste per tutti i tuoi account Google Ads. Recupera il token sviluppatore tramite [accesso al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi alla pagina API Center. |
| Aggiorna token | Il token di aggiornamento fa parte di [!DNL OAuth2] autenticazione. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| ID client | L&#39;ID client viene utilizzato in tandem con il segreto client come parte di [!DNL OAuth2] autenticazione. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto del tuo account identificando l&#39;applicazione in Google. |
| Segreto client | Il segreto client viene utilizzato in parallelo con l’ID client come parte di [!DNL OAuth2] autenticazione. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto del tuo account identificando l&#39;applicazione in Google. |

Leggi il documento di panoramica API per [ulteriori informazioni su come iniziare a utilizzare Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Collegare l&#39;account Google Ads

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Pubblicità]** categoria, seleziona **[!UICONTROL Google Ads]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle sorgenti nell’interfaccia utente Experience Platform.](../../../../images/tutorials/create/ads/catalog.png).

La **[!UICONTROL Connetti a Google Ads]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona l’account Google Ads con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![La pagina di selezione degli account esistenti nel flusso di lavoro origini.](../../../../images/tutorials/create/ads/existing.png).

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali Google Ads. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![La nuova interfaccia account nel flusso di lavoro origini.](../../../../images/tutorials/create/ads/new.png).

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account Google Ads. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati pubblicitari in Platform](../../dataflow/advertising.md).
