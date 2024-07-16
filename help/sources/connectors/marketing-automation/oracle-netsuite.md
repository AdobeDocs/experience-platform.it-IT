---
title: Panoramica di Oracle NetSuite Source
description: Scopri come collegare Oracle NetSuite a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 2%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>L&#39;origine [!DNL Oracle NetSuite] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione dei dati da parte di sistemi di automazione del marketing di terze parti. Il supporto per i provider di automazione marketing include [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) è una suite di gestione aziendale basata su cloud che include soluzioni ERP/finanziarie, CRM ed e-commerce.

È possibile utilizzare due origini diverse per acquisire i dati da [!DNL Oracle NetSuite] all&#39;Experience Platform:

* Utilizza l&#39;origine [!DNL Oracle NetSuite Activities] per acquisire i dati degli eventi.
* Utilizza l&#39;origine [!DNL Oracle NetSuite Entities] per acquisire i dati dei clienti e dei contatti.

Per ulteriori informazioni sulle due origini [!DNL Oracle NetSuite], vedere la tabella seguente.

| Origine | Tipo | Descrizione |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupera le attività pianificate aggiunte al calendario. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupera dati cliente specifici, inclusi dettagli quali nomi, indirizzi e identificatori chiave del cliente. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contatto | Recupera i nomi dei contatti, le e-mail, i numeri di telefono ed eventuali campi personalizzati relativi ai contatti associati ai clienti. |

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Prerequisiti {#prerequisites}

Prima di poter portare i dati di [!DNL Oracle NetSuite] all&#39;Experience Platform, è necessario assicurarsi di disporre dei seguenti elementi:

* **Un account [!DNL Oracle NetSuite]**.
   * Contattare [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) se non si dispone già di un account valido.
* Una **sottoscrizione attiva** a qualsiasi prodotto [!DNL Oracle NetSuite].
* Un **ID account**.
   * L&#39;origine [!DNL Oracle NetSuite] utilizza OAuth 2.0 per comunicare con le API [!DNL Oracle NetSuite]. Se non disponi del tuo ID account, visita la documentazione di [!DNL Oracle] su [come recuperare l&#39;ID account](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Combinazione di **ID client** e **segreto client**.
   * Per accedere alle API [!DNL Oracle NetSuite] sono necessari l&#39;ID client e il segreto client. Durante questo passaggio, devi anche assicurarti che l’amministratore disponga di:
      * Abilitazione della funzione OAuth 2.0 e configurazione dei ruoli OAuth 2.0 appropriati.
      * Assegnazione degli utenti ai ruoli OAuth 2.0 e creazione dei record di integrazione necessari.
* Un **token di accesso** e un **token di aggiornamento**.
   * Per informazioni su come generare i token di accesso e aggiornamento, consulta la guida di [!DNL Oracle] in [Flusso di concessione codice di autorizzazione OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow).

### Raccogli le credenziali richieste {#gather-credentials}

Per connettere [!DNL Oracle NetSuite] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID client | Valore ID client generato quando si crea il record di integrazione in [!DNL Oracle NetSuite]. Per ulteriori informazioni, leggere la guida di [!DNL Oracle] su come [creare record di integrazione](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). | `7fce.....b42f`<br>Il valore è una stringa di 64 caratteri. |
| Segreto client | Il valore segreto client generato quando crei il record di integrazione. Per ulteriori informazioni, leggere la guida di [!DNL Oracle] su come [creare record di integrazione](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). | `5c98.....1b46`<br>Il valore è una stringa di 64 caratteri. |
| URL test di autorizzazione | (Facoltativo) URL del test di autorizzazione [!DNL NetSuite]. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token di accesso | Il token di accesso è in formato JSON Web Token (JWT) ed è valido solo per 60 minuti. Per ulteriori informazioni su come recuperare il token di accesso, leggere la guida di [!DNL Oracle] in [Autorizzazione OAuth 2.0 per NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Il valore è una stringa di 1024 caratteri formattata come JSON Web Token (JWT). |
| Aggiorna token | Utilizza l’aggiornamento per generare un nuovo token di accesso, dopo la scadenza del token di accesso. Il token di aggiornamento è valido per sette giorni. Per ulteriori informazioni su come recuperare il token di accesso, leggere la guida di [!DNL Oracle] in [Autorizzazione OAuth 2.0 per NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Il valore è una stringa di 1024 caratteri formattata come JSON Web Token (JWT). |
| URL token di accesso | Endpoint token a cui l’applicazione invia le richieste POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Dopo la scadenza di un token di aggiornamento, devi creare un nuovo account in Experience Platform con i token aggiornati.

## Connetti [!DNL Oracle NetSuite Activities] a Platform {#oracle-netsuite-activities}

La documentazione seguente fornisce informazioni su come connettere [!DNL Oracle NetSuite Activities] a Platform tramite API o tramite l&#39;interfaccia utente:

* [Crea una connessione di origine e un flusso di dati per portare [!DNL Oracle NetSuite Activities] dati in Platform tramite API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Connetti il tuo account [!DNL Oracle NetSuite Activities] ad Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Creare un flusso di dati per una connessione di origine utilizzando l&#39;interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).

## Connetti [!DNL Oracle NetSuite Entities] a Platform {#oracle-netsuite-entities}

La documentazione seguente fornisce informazioni su come connettere [!DNL Oracle NetSuite Entities] a Platform tramite API o tramite l&#39;interfaccia utente:

* [Crea una connessione di origine e un flusso di dati per portare [!DNL Oracle NetSuite Entities] dati in Platform tramite API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Connetti il tuo account [!DNL Oracle NetSuite Entities] ad Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Creare un flusso di dati per una connessione di origine utilizzando l&#39;interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).
