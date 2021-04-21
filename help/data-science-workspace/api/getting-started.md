---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;data science workspace;scienza dei dati
solution: Experience Platform
title: Guida all’API di apprendimento automatico di Sensei
topic-legacy: Developer guide
description: L’API di apprendimento automatico Sensei consente agli sviluppatori di eseguire operazioni CRUD su varie risorse di Data Science Workspace. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] Guida all’API

L’ API [!DNL Sensei Machine Learning] fornisce un meccanismo che consente agli scienziati dei dati di organizzare e gestire i servizi di apprendimento automatico, dall’onboarding degli algoritmi alla sperimentazione e alla distribuzione dei servizi.

Questa guida per gli sviluppatori descrive i passaggi necessari per iniziare a utilizzare [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) e illustra le chiamate API per eseguire operazioni CRUD su varie risorse di Data Science Workspace.

## Introduzione

Devi aver completato l&#39;esercitazione [authentication](https://www.adobe.com/go/platform-api-authentication-en) per poter accedere alle seguenti intestazioni di richiesta per effettuare chiamate alle API [!DNL Adobe Experience Platform] :

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* nome x-sandbox: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Passaggi successivi

Una volta raccolte le credenziali di autenticazione richieste, puoi procedere alle sezioni successive di questa guida per sviluppatori per le chiamate API di esempio ai seguenti gruppi di endpoint:

* [Motori](./engines.md)
* [Esperimenti](./experiments.md)
* [Informazioni approfondite](./insights.md)
* [MLI (ricette)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelli](./models.md)
* [Appendice](./appendix.md)
