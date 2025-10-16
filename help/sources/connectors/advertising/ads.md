---
title: Panoramica di Google Ads Source
description: Scopri come collegare Google Ads a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: a0977e98219797eda14dd8d7ddb6cf3f1410cef0
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 5%

---

# Origine [!DNL Google Ads]

>[!NOTE]
>
>L&#39;origine [!DNL Google Ads] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Il supporto per i provider pubblicitari include [!DNL Google Ads].

## Prerequisiti {#prerequisites}

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account **[!UICONTROL ad Experience Platform, è necessario che per l&#39;account siano abilitate le autorizzazioni]** Visualizza origini **[!UICONTROL e]** Gestisci origini[!DNL Google Ads]. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

### Raccogli le credenziali richieste

Per connettere correttamente l&#39;account [!DNL Google Ads] ad Experience Platform, è necessario fornire i valori appropriati alle credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| `clientCustomerId` | L&#39;ID cliente client è il numero di account corrispondente all&#39;account client [!DNL Google Ads] che si desidera gestire con l&#39;API [!DNL Google Ads]. Questo ID segue il modello di `123-456-7890`. |
| `loginCustomerId` | L&#39;ID cliente di accesso è il numero di account che corrisponde all&#39;account manager [!DNL Google Ads] e viene utilizzato per recuperare i dati del report da un cliente operativo specifico. Per ulteriori informazioni sull&#39;ID cliente di accesso, leggere la [[!DNL Google Ads] documentazione API](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | Il token sviluppatore consente di accedere all&#39;API [!DNL Google Ads]. Puoi utilizzare lo stesso token sviluppatore per effettuare richieste su tutti gli account [!DNL Google Ads]. Recupera il token di sviluppo [accedendo al tuo account manager](https://ads.google.com/home/tools/manager-accounts/) e quindi passando alla pagina [!DNL API Center]. |
| `refreshToken` | Il token di aggiornamento fa parte dell&#39;autenticazione [!DNL OAuth2]. Questo token ti consente di rigenerare i token di accesso dopo la scadenza. |
| `clientId` | L&#39;ID client viene utilizzato insieme al segreto client come parte dell&#39;autenticazione [!DNL OAuth2]. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Google]. |
| `clientSecret` | Il segreto client viene utilizzato insieme all&#39;ID client come parte dell&#39;autenticazione [!DNL OAuth2]. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Google]. |
| `googleAdsApiVersion` | La versione API corrente supportata da [!DNL Google Ads]. Sebbene la versione più recente dell&#39;API [!DNL Google Ads] sia la v21, Experience Platform attualmente supporta la versione v19 e successive. Assicurati di utilizzare una di queste versioni supportate per garantire la compatibilità. |
| `connectionSpec.id` | La specifica di connessione restituisce le proprietà del connettore di un&#39;origine, incluse le specifiche di autenticazione relative alla creazione delle connessioni di base e di origine. ID della specifica di connessione per [!DNL Google Ads]: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Questo valore è necessario se si connette l&#39;account [!DNL Google Ads] tramite l&#39;API [!DNL Flow Service]. |

## Connetti [!DNL Google Ads] ad Experience Platform

La documentazione seguente fornisce informazioni su come connettere [!DNL Google Ads] ad Experience Platform tramite API o tramite l&#39;interfaccia utente:

### Utilizzo delle API

* [Creare una connessione di base Google Ads utilizzando l’API del servizio Flusso](../../tutorials/api/create/advertising/ads.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine pubblicitaria utilizzando l’API del servizio Flow](../../tutorials/api/collect/advertising.md)

### Utilizzo dell’interfaccia utente

* [Creare una connessione sorgente Google Ads nell’interfaccia utente](../../tutorials/ui/create/advertising/ads.md)
* [Creare un flusso di dati per una connessione sorgente per annunci pubblicitari nell’interfaccia utente](../../tutorials/ui/dataflow/advertising.md)
