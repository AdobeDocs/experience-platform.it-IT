---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Guida per gli sviluppatori di API Sensei Machine Learning
topic: Developer guide
description: Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l'API Sensei Machine Learning e illustra le chiamate API per l'esecuzione di operazioni CRUD su varie risorse di Data Science Workspace.
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] Guida per gli sviluppatori di API

L&#39; [!DNL Sensei Machine Learning] API fornisce agli esperti di dati un meccanismo per organizzare e gestire i servizi di machine learning, dall&#39;installazione degli algoritmi alla sperimentazione e all&#39;implementazione dei servizi.

Questa guida per gli sviluppatori illustra i passaggi necessari per iniziare a utilizzare [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)e illustra le chiamate API per l&#39;esecuzione di operazioni CRUD su varie risorse di Data Science Workspace.

## Introduzione

È necessario completare l&#39;esercitazione sull&#39; [autenticazione](../../tutorials/authentication.md) per poter accedere alle seguenti intestazioni di richiesta per effettuare chiamate alle [!DNL Adobe Experience Platform] API:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Dopo aver raccolto le credenziali di autenticazione richieste, potete procedere alle sezioni successive di questa guida per gli sviluppatori per le chiamate API di esempio ai seguenti gruppi di endpoint:

* [Motori](./engines.md)
* [Esperimenti](./experiments.md)
* [Approfondimenti](./insights.md)
* [MLInances (Ricette)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [Modelli](./models.md)
* [Appendice](./appendix.md)