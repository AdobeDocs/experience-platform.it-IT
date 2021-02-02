---
keywords: ' Experience Platform;home;argomenti popolari;intervallo date'
solution: Experience Platform
title: Guida introduttiva all'API Observability Insights
topic: developer guide
description: L'API Observability Insights consente di recuperare dati delle metriche per diverse funzionalità di Adobe Experience Platform. Questo documento fornisce un'introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all'API Observability Insights.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Guida introduttiva all&#39;API [!DNL Observability Insights]

L&#39;API [!DNL Observability Insights] consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all&#39;API [!DNL Observability Insights].

## Lettura di chiamate API di esempio

La documentazione API [!DNL Observability Insights] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa alla lettura delle chiamate API di esempio nella [ guida alla risoluzione dei problemi del Experience Platform](../../landing/troubleshooting.md).

## Intestazioni necessarie

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Observability Insights], andate alla guida [agli endpoint delle metriche](./metrics.md).