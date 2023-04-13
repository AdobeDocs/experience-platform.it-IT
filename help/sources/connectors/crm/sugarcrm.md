---
title: Panoramica origine SugarCRM
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
>La [!DNL SugarCRM] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati da un’applicazione CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) è un sistema di gestione delle relazioni con i clienti (CRM). [!DNL SugarCRM]Le funzionalità di includono automazione delle forze di vendita, campagne di marketing, supporto clienti, collaborazione, Mobile CRM, Social CRM e reporting.

La [!DNL SugarCRM] source consente di acquisire account, contatti ed eventi dai seguenti endpoint API:

* [Account](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contatti](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventi](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] utilizza i token portatori come meccanismo di autenticazione per comunicare con [!DNL SugarCRM] API account e contatti e [!DNL SugarCRM] API eventi.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti

Prima di creare un [!DNL SugarCRM] connessione di origine, è innanzitutto necessario assicurarsi di disporre dei seguenti elementi:

* A [!DNL SugarMarket] conto. Devi contattare il tuo [!DNL SugarCRM] account manager per ottenere un [!DNL SugarMarket] se non ne hai già uno.

* Un nome utente e un account API univoci separato da qualsiasi account utente associato al processo di marketing o vendita. Questa combinazione di nome utente e account univoci deve disporre di autorizzazioni di accesso API. Per ulteriori informazioni sul processo di configurazione di un account, visita il [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentazione.

## Connetti [!DNL SugarCRM Accounts & Contacts] su Platform

* [Crea una connessione sorgente da portare [!DNL SugarCRM Accounts & Contacts] dati su Platform tramite API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Crea una connessione sorgente da portare [!DNL SugarCRM Accounts & Contacts] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio di flusso](../../tutorials/api/collect/crm.md)


## Connetti [!DNL SugarCRM Events] su Platform

* [Crea una connessione sorgente da portare [!DNL SugarCRM Events] dati su Platform tramite API](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Crea una connessione sorgente da portare [!DNL SugarCRM Events] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Creare un flusso di dati per una connessione sorgente CRM nell&#39;interfaccia utente](../../tutorials/ui/dataflow/crm.md)
