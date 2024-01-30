---
title: Panoramica sull'origine di Oracle NetSuite
description: Scopri come collegare Oracle NetSuite a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>Il [!DNL Oracle NetSuite] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experienci Platform fornisce supporto per l’acquisizione dei dati da parte di sistemi di automazione del marketing di terze parti. Il supporto per i provider di automazione marketing include [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) è una suite di gestione aziendale basata su cloud che include soluzioni ERP/finanziarie, di gestione delle relazioni con i clienti e di e-commerce.

Puoi utilizzare due origini diverse per acquisire i dati da [!DNL Oracle NetSuite] ad Experience Platform:

* Utilizza il [!DNL Oracle NetSuite Activities] origine per acquisire i dati degli eventi.
* Utilizza il [!DNL Oracle NetSuite Entities] per acquisire i dati di clienti e contatti.

Per ulteriori informazioni sulle due opzioni, consulta la tabella seguente [!DNL Oracle NetSuite] origini.

| Origine | Tipo | Descrizione |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupera le attività pianificate aggiunte al calendario. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupera dati cliente specifici, inclusi dettagli quali nomi, indirizzi e identificatori chiave del cliente. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contatto | Recupera i nomi dei contatti, le e-mail, i numeri di telefono ed eventuali campi personalizzati relativi ai contatti associati ai clienti. |

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti {#prerequisites}

Prima di poter portare il [!DNL Oracle NetSuite] dati per Experience Platform, devi prima assicurarti di disporre dei seguenti elementi:

* **Un [!DNL Oracle NetSuite] account**.
   * Contatto [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) se non disponi già di un account valido.
* Un **abbonamento attivo** a qualsiasi [!DNL Oracle NetSuite] prodotto.
* Un **ID account**.
   * Il [!DNL Oracle NetSuite] origine utilizza OAuth 2.0 per comunicare con [!DNL Oracle NetSuite] API. Se non disponi del tuo ID account, visita [!DNL Oracle] documentazione su [come recuperare l’ID account](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **ID client** e **segreto client** combinazione.
   * Per accedere a sono necessari l’ID client e il segreto client [!DNL Oracle NetSuite] API. Durante questo passaggio, devi anche assicurarti che l’amministratore disponga di:
      * Abilitazione della funzione OAuth 2.0 e configurazione dei ruoli OAuth 2.0 appropriati.
      * Assegnazione degli utenti ai ruoli OAuth 2.0 e creazione dei record di integrazione necessari.
* Un **token di accesso** e un **aggiorna token**.
   * Consulta la sezione [!DNL Oracle] guida su [Flusso di concessione codice di autorizzazione OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) per informazioni su come generare i token di accesso e aggiornamento.

### Raccogli le credenziali richieste {#gather-credentials}

Per connettersi [!DNL Oracle NetSuite] In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID client | Il valore ID client generato quando crei il record di integrazione in [!DNL Oracle NetSuite]. Leggi le [!DNL Oracle] guida su come [creare record di integrazione](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) per ulteriori informazioni. | `7fce.....b42f`<br>Il valore è una stringa di 64 caratteri. |
| Segreto client | Il valore segreto client generato quando crei il record di integrazione. Leggi le [!DNL Oracle] guida su come [creare record di integrazione](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) per ulteriori informazioni. | `5c98.....1b46`<br>Il valore è una stringa di 64 caratteri. |
| URL test di autorizzazione | (Facoltativo) Il [!DNL NetSuite] URL del test di autorizzazione. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token di accesso | Il token di accesso è in formato JSON Web Token (JWT) ed è valido solo per 60 minuti. Per ulteriori informazioni su come recuperare il token di accesso, leggi [!DNL Oracle] guida su [Autorizzazione OAuth 2.0 per NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> Il valore è una stringa di 1024 caratteri formattata come JSON Web Token (JWT). |
| Aggiorna token | Utilizza l’aggiornamento per generare un nuovo token di accesso, dopo la scadenza del token di accesso. Il token di aggiornamento è valido per sette giorni. Per ulteriori informazioni su come recuperare il token di accesso, leggi [!DNL Oracle] guida su [Autorizzazione OAuth 2.0 per NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> Il valore è una stringa di 1024 caratteri formattata come JSON Web Token (JWT). |
| URL token di accesso | Endpoint token a cui l’applicazione invia le richieste POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Dopo la scadenza di un token di aggiornamento, devi creare un nuovo account in Experienci Platform con i token aggiornati.

## Connetti [!DNL Oracle NetSuite Activities] alla piattaforma {#oracle-netsuite-activities}

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Oracle NetSuite Activities] in Platform tramite API o l’interfaccia utente:

* [Creare una connessione di origine e un flusso di dati per portare [!DNL Oracle NetSuite Activities] dati per Platform tramite API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Connetti [!DNL Oracle NetSuite Activities] Experience Platform dell’account tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Creare un flusso di dati per una connessione sorgente utilizzando l’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).

## Connetti [!DNL Oracle NetSuite Entities] alla piattaforma {#oracle-netsuite-entities}

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Oracle NetSuite Entities] in Platform tramite API o l’interfaccia utente:

* [Creare una connessione di origine e un flusso di dati per portare [!DNL Oracle NetSuite Entities] dati per Platform tramite API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Connetti [!DNL Oracle NetSuite Entities] Experience Platform dell’account tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Creare un flusso di dati per una connessione sorgente utilizzando l’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).
