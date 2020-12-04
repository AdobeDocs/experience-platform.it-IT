---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Guida introduttiva all'API Observability Insights
topic: developer guide
description: L'API Observability Insights consente di recuperare dati delle metriche per diverse funzionalità di Adobe Experience Platform. Questo documento fornisce un'introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all'API Observability Insights.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Getting started with the [!DNL Observability Insights] API

L&#39; [!DNL Observability Insights] API consente di recuperare i dati delle metriche per diverse funzionalità di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all&#39; [!DNL Observability Insights] API.

## Lettura di chiamate API di esempio

La documentazione [!DNL Observability Insights] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa alla lettura delle chiamate API di esempio nella guida alla risoluzione dei problemi del [Experience Platform](../../landing/troubleshooting.md).

## Intestazioni necessarie

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39; [!DNL Observability Insights] API, andate alla guida [dell&#39;endpoint](./metrics.md)delle metriche.