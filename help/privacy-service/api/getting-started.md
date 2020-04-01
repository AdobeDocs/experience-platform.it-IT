---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori del servizio sulla privacy
description: Utilizza l’API RESTful per gestire i dati personali dei tuoi soggetti di dati nelle applicazioni Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a28ad2725094e0748e2860276ab2e7581d790ac

---


# Guida per gli sviluppatori del servizio sulla privacy

Il servizio per la privacy di Adobe Experience Platform fornisce un’API RESTful e un’interfaccia utente che consentono di gestire (accedere ed eliminare) i dati personali dei tuoi soggetti dati (clienti) nelle applicazioni Adobe Experience Cloud. Il servizio Privacy fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono le applicazioni Experience Cloud.

Questa guida illustra come utilizzare l’API del servizio per la privacy. Per informazioni dettagliate sull’utilizzo dell’interfaccia utente, consultate la panoramica [dell’interfaccia utente del servizio](../ui/overview.md)per la privacy. Per un elenco completo di tutti gli endpoint disponibili nell&#39;API del servizio sulla privacy, consultate il riferimento [](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Introduzione

Questa guida richiede una buona conoscenza delle seguenti funzionalità della piattaforma Experience:

* [Servizio](../home.md)Privacy: Fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire l&#39;accesso e l&#39;eliminazione delle richieste dai soggetti dati (clienti) nelle applicazioni Adobe Experience Cloud.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate all&#39;API del servizio sulla privacy.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](https://www.adobe.io/apis/experienceplatform/home/services/troubleshooting.html#!api-specification/markdown/narrative/technical_overview/platform_faq_and_troubleshooting/platform_faq_and_troubleshooting.md) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API della piattaforma, dovete prima completare l&#39;esercitazione [di](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Ora che hai capito quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all’API del servizio sulla privacy. Il documento sui processi [di](privacy-jobs.md) privacy illustra le varie chiamate API che potete effettuare tramite l’API del servizio Privacy. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.
