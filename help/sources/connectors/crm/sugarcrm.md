---
title: Panoramica dell’origine di SugarCRM
description: Scopri come collegare SugarCRM a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (Beta) [!DNL SugarCRM]

>[!NOTE]
>
>Il [!DNL SugarCRM] sorgente in versione beta. Consulta la [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione CRM di terze parti. Il supporto per i provider CRM include [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) è un sistema di gestione delle relazioni con i clienti (CRM). [!DNL SugarCRM]Le funzionalità di includono automazione per la forza vendita, campagne di marketing, supporto clienti, collaborazione, gestione delle relazioni con i clienti tramite dispositivi mobili, gestione delle relazioni con i clienti social e reporting.

Il [!DNL SugarCRM] La sorgente consente di acquisire i dati di account, contatti ed eventi dai seguenti endpoint API:

* [Account](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contatti](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventi](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] utilizza token Bearer come meccanismo di autenticazione per comunicare con [!DNL SugarCRM] API di account e contatti e [!DNL SugarCRM] Eventi API.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti

Prima di creare un [!DNL SugarCRM] connessione di origine, è necessario verificare di disporre dei seguenti elementi:

* A [!DNL SugarMarket] account. È necessario contattare il [!DNL SugarCRM] account manager per ottenere un [!DNL SugarMarket] se non ne hai già uno.

* Un nome utente e un account API univoci, separati da tutti gli account utente associati al processo di marketing o vendita. Questa combinazione univoca di nome utente e account deve disporre di autorizzazioni di accesso API. Per ulteriori informazioni sul processo di configurazione di un account, visita [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentazione.

## Connetti [!DNL SugarCRM Accounts & Contacts] alla piattaforma

* [Crea una connessione sorgente da portare [!DNL SugarCRM Accounts & Contacts] dati per Platform tramite API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Crea una connessione sorgente da portare [!DNL SugarCRM Accounts & Contacts] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)


## Connetti [!DNL SugarCRM Events] alla piattaforma

* [Crea una connessione sorgente da portare [!DNL SugarCRM Events] dati per Platform tramite API](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Crea una connessione sorgente da portare [!DNL SugarCRM Events] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Creare un flusso di dati per una connessione di origine CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
