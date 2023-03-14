---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Marketing Cloud Salesforce;automazione marketing
solution: Experience Platform
title: Panoramica sull’origine del Marketing Cloud Salesforce
description: Scopri come collegare il Marketing Cloud Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# (Beta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>Il [!DNL Salesforce Marketing Cloud] sorgente in versione beta. Consulta la [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[!DNL Experience Platform] fornisce supporto per l’acquisizione di dati da sistemi di automazione del marketing di terze parti. Il supporto per i provider di automazione marketing include [!DNL Salesforce Marketing Cloud].

## Prerequisiti

Prima di collegare il [!DNL Salesforce Marketing Cloud] da sorgente a Platform, è necessario assicurarsi che i seguenti **ambiti di autorizzazione** dispongono del provisioning per [!DNL Salesforce Marketing Cloud] combinazione di ID client e segreto client:

* `campaign_read`
* `list_and_subscribers_read`

Puoi richiedere gli ambiti effettuando una chiamata al `v2/userinfo` risorsa del [!DNL Salesforce Marketing Cloud] API. Consulta la [[!DNL Salesforce Marketing Cloud] Documento Ambiti di autorizzazione dell’integrazione API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) per informazioni su come richiedere e confrontare gli ambiti.

Per ulteriori informazioni sugli ambiti, incluso un elenco delle autorizzazioni e dei comportamenti correlati, consulta [[!DNL Salesforce Marketing Cloud] Documento REST API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Connetti [!DNL Salesforce Marketing Cloud] alla piattaforma utilizzando le API

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Salesforce Marketing Cloud] alla piattaforma che utilizza le API:

* [Creare una connessione di base al Marketing Cloud Salesforce utilizzando l’API del servizio Flow](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di automazione marketing utilizzando l’API del servizio Flusso](../../tutorials/api/collect/marketing-automation.md)

## Connetti [!DNL Salesforce Marketing Cloud] a Platform tramite l’interfaccia utente

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Salesforce Marketing Cloud] a Platform utilizzando l’interfaccia utente:

* [Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Creare un flusso di dati per una connessione sorgente dell’automazione marketing nell’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md)
