---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti popolari;data science workspace;data science
solution: Experience Platform
title: Guida API di apprendimento automatico di Sensei
description: L’API di apprendimento automatico di Sensei consente agli sviluppatori di eseguire operazioni CRUD su varie risorse di Data Science Workspace. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 15%

---

# Guida dell’API di [!DNL Sensei Machine Learning]

L&#39;API [!DNL Sensei Machine Learning] fornisce un meccanismo che consente ai data scientist di organizzare e gestire i servizi di machine learning, dall&#39;onboarding degli algoritmi alla sperimentazione e alla distribuzione dei servizi.

Questa guida per gli sviluppatori descrive i passaggi necessari per iniziare a utilizzare l&#39;[API di apprendimento automatico di Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) e illustra le chiamate API per l&#39;esecuzione di operazioni CRUD su varie risorse Workspace di Data Science.

## Introduzione

È necessario aver completato l&#39;esercitazione di [autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per poter accedere alle intestazioni di richiesta seguenti per effettuare chiamate alle API [!DNL Adobe Experience Platform]:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Dopo aver raccolto le credenziali di autenticazione richieste, puoi passare alle sezioni successive di questa guida per sviluppatori per esempi di chiamate API ai seguenti gruppi di endpoint:

* [Motori](./engines.md)
* [Esperimenti](./experiments.md)
* [Approfondimenti](./insights.md)
* [MLInstance (ricette)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelli](./models.md)
* [Appendice](./appendix.md)
