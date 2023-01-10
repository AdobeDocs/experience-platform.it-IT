---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Marketing Cloud Salesforce;automazione marketing
solution: Experience Platform
title: Panoramica della sorgente del Marketing Cloud Salesforce
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
>La [!DNL Salesforce Marketing Cloud] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da sistemi di automazione marketing di terze parti. Il supporto per i fornitori di automazione del marketing include: [!DNL Salesforce Marketing Cloud].

## Prerequisiti

Prima di poter collegare le [!DNL Salesforce Marketing Cloud] da sorgente a Platform, è necessario assicurarsi che quanto segue **ambiti di autorizzazione** dispongono del provisioning [!DNL Salesforce Marketing Cloud] combinazione di ID client e segreto client:

* `campaign_read`
* `list_and_subscribers_read`

Puoi richiedere gli ambiti effettuando una chiamata al `v2/userinfo` della risorsa [!DNL Salesforce Marketing Cloud] API. Consulta la sezione [[!DNL Salesforce Marketing Cloud] Documento sugli ambiti delle autorizzazioni di integrazione API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) per informazioni su come richiedere e confrontare gli ambiti.

Per ulteriori informazioni sugli ambiti, compreso un elenco delle relative autorizzazioni e dei relativi comportamenti, consulta [[!DNL Salesforce Marketing Cloud] Documento API REST](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Connetti [!DNL Salesforce Marketing Cloud] su Platform tramite API

La documentazione seguente fornisce informazioni su come connettersi [!DNL Salesforce Marketing Cloud] su Platform tramite API:

* [Creare una connessione di base al Marketing Cloud Salesforce utilizzando l’API del servizio di flusso](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio di flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di automazione del marketing utilizzando l’API del servizio di flusso](../../tutorials/api/collect/marketing-automation.md)

## Connetti [!DNL Salesforce Marketing Cloud] su Platform tramite l’interfaccia utente

La documentazione seguente fornisce informazioni su come connettersi [!DNL Salesforce Marketing Cloud] su Platform utilizzando l’interfaccia utente di :

* [Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Creare un flusso di dati per una connessione sorgente di automazione marketing nell’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md)
