---
title: Panoramica di Salesforce Marketing Cloud Source
description: Scopri come collegare Salesforce Marketing Cloud a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>L&#39;origine [!DNL Oracle Salesforce Marketing Cloud] è ora obsoleta e non è più disponibile. Utilizza la nuova origine [[!DNL Salesforce Marketing Cloud] (V2)](sfmc.md) come nuovo connettore per i dati [!DNL Salesforce Marketing Cloud].

[!DNL Salesforce Marketing Cloud] consente di gestire e automatizzare il coinvolgimento dei clienti tramite e-mail, dispositivi mobili, social media e annunci pubblicitari, il tutto da un&#39;unica piattaforma. Con strumenti come E-mail Studio, Percorsi Builder e Audience Builder, puoi creare campagne personalizzate e percorsi di clienti su misura per il tuo pubblico.

È possibile utilizzare l&#39;origine [!DNL Salesforce Marketing Cloud] per connettere l&#39;account e trasferire i dati in Adobe Experience Platform.

## Prerequisiti

Prima di poter connettere l&#39;origine [!DNL Salesforce Marketing Cloud] ad Experience Platform, è necessario assicurarsi che sia stato eseguito il provisioning dei seguenti **ambiti di autorizzazione** per l&#39;ID client [!DNL Salesforce Marketing Cloud] e la combinazione di segreto client:

* `campaign_read`
* `list_and_subscribers_read`

È possibile richiedere ambiti effettuando una chiamata alla risorsa `v2/userinfo` dell&#39;API [!DNL Salesforce Marketing Cloud]. Per istruzioni su come richiedere e confrontare gli ambiti, consulta il documento [[!DNL Salesforce Marketing Cloud] Ambiti di autorizzazione dell&#39;integrazione API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>).

Per ulteriori informazioni sugli ambiti, incluso un elenco delle autorizzazioni e dei comportamenti correlati, vedere questo [[!DNL Salesforce Marketing Cloud] documento REST API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Se non si aggiungono gli indirizzi IP necessari al inserisco nell&#39;elenco Consentiti di, l&#39;account [!DNL Salesforce Marketing Cloud] non si connette ad Experience Platform.

### Autenticazione in Experience Platform su Azure {#azure}

Per connettere [!DNL Salesforce Marketing Cloud] ad Experience Platform il [!DNL Azure] è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| Host | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il valore `host`, è necessario specificare `{subdomain}.rest.marketingcloudapis.com`. Ad esempio, se l&#39;URL host è `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è necessario immettere `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` come valore host. |
| ID client | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| Segreto client | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| ID specifica di connessione | La **specifica di connessione** fornisce le proprietà del connettore di un&#39;origine dati. Ciò include dettagli quali le specifiche di autenticazione e i requisiti per la creazione di connessioni **base** e **source**. Per [!DNL Salesforce Marketing Cloud], l&#39;ID della specifica di connessione è: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Nota:** questa credenziale è necessaria solo per la connessione tramite API. |

### Autenticazione per Experience Platform su Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Questa sezione si applica alle implementazioni di Experience Platform in esecuzione su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../landing/multi-cloud.md).

Per connettere [!DNL Salesforce Marketing Cloud] ad Experience Platform su AWS è necessario fornire i valori per le credenziali seguenti.

| Credenziali | Descrizione |
| --- | --- |
| Sottodominio | Parte univoca dell&#39;URL dell&#39;istanza [!DNL Salesforce Marketing Cloud], utilizzata per creare endpoint API. |
| ID client | Un identificatore pubblico per l&#39;applicazione, generato quando si crea un pacchetto installato in [!DNL Salesforce Marketing Cloud] |
| Segreto client | Una chiave riservata associata al tuo ID client, generata anche nel pacchetto installato. |
| ID specifica di connessione | La **specifica di connessione** fornisce le proprietà del connettore di un&#39;origine dati. Ciò include dettagli quali le specifiche di autenticazione e i requisiti per la creazione di connessioni **base** e **source**. Per [!DNL Salesforce Marketing Cloud], l&#39;ID della specifica di connessione è: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Nota:** questa credenziale è necessaria solo per la connessione tramite API. |

Per ulteriori informazioni, leggere la [[!DNL Salesforce] documentazione sul token di accesso per le integrazioni server-to-server](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite API:

* [Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di automazione marketing utilizzando l’API del servizio Flusso](../../tutorials/api/collect/marketing-automation.md)

## Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite l&#39;interfaccia utente

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite l&#39;interfaccia utente:

* [Connetti [!DNL Salesforce Marketing Cloud] ad Experience Platform nell&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Creare un flusso di dati per una connessione sorgente dell’automazione marketing nell’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md)
