---
title: Panoramica di SugarCRM Source
description: Scopri come collegare SugarCRM a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) è un sistema CRM (Customer Relationship Management). Le funzionalità di [!DNL SugarCRM] includono automazione della forza vendita, campagne di marketing, supporto clienti, collaborazione, CRM mobile, CRM social e reporting.

L&#39;origine [!DNL SugarCRM] consente di acquisire i dati di account, contatti ed eventi dai seguenti endpoint API:

* [Account](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contatti](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventi](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] utilizza token Bearer come meccanismo di autenticazione per comunicare con le API Account e Contatto [!DNL SugarCRM] e con l&#39;API degli eventi [!DNL SugarCRM].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Prerequisiti

Prima di poter creare una connessione di origine [!DNL SugarCRM], è necessario verificare di disporre dei seguenti elementi:

* Un account [!DNL SugarMarket]. Contattare l&#39;account manager di [!DNL SugarCRM] per ottenere un account di [!DNL SugarMarket] valido, se non ne si dispone già.

* Un nome utente e un account API univoci, separati da tutti gli account utente associati al processo di marketing o vendita. Questa combinazione univoca di nome utente e account deve disporre di autorizzazioni di accesso API. Per ulteriori informazioni sul processo di configurazione di un account, vedere la documentazione di [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro).

## Connetti [!DNL SugarCRM Accounts & Contacts] a Platform

* [Crea una connessione di origine per portare [!DNL SugarCRM Accounts & Contacts] dati a Platform tramite API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Crea una connessione di origine per portare [!DNL SugarCRM Accounts & Contacts] dati a Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)


## Connetti [!DNL SugarCRM Events] a Platform

* [Crea una connessione di origine per portare [!DNL SugarCRM Events] dati a Platform tramite API](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Crea una connessione di origine per portare [!DNL SugarCRM Events] dati a Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Creare un flusso di dati per una connessione di origine CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
