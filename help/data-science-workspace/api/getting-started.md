---
keywords: Experience Platform;guida per sviluppatori;endpoint;Data Science Workspace;argomenti comuni;data science workspace;scienza dei dati
solution: Experience Platform
title: Guida all’API di apprendimento automatico di Sensei
description: L’API di apprendimento automatico di Sensei consente agli sviluppatori di eseguire operazioni CRUD su varie risorse di Data Science Workspace. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---

# Guida dell’API di [!DNL Sensei Machine Learning]

La [!DNL Sensei Machine Learning] L’API fornisce un meccanismo che consente agli scienziati dei dati di organizzare e gestire i servizi di apprendimento automatico, dall’onboarding degli algoritmi alla sperimentazione e alla distribuzione dei servizi.

Questa guida per gli sviluppatori descrive i passaggi necessari per iniziare a utilizzare [API di apprendimento automatico di Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), e illustra le chiamate API per l’esecuzione di operazioni CRUD su varie risorse di Data Science Workspace.

## Introduzione

Devi aver completato il [autenticazione](https://www.adobe.com/go/platform-api-authentication-en) tutorial per poter accedere alle seguenti intestazioni di richiesta a cui effettuare chiamate [!DNL Adobe Experience Platform] API:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Passaggi successivi

Una volta raccolte le credenziali di autenticazione richieste, puoi procedere alle sezioni successive di questa guida per sviluppatori per le chiamate API di esempio ai seguenti gruppi di endpoint:

* [Motori](./engines.md)
* [Esperimenti](./experiments.md)
* [Insights](./insights.md)
* [MLI (ricette)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelli](./models.md)
* [Appendice](./appendix.md)
