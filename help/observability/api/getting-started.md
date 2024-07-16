---
keywords: Experience Platform;home;argomenti popolari;intervallo date
solution: Experience Platform
title: Guida introduttiva all’API Observability Insights
description: L’API Observability Insights consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 18%

---

# Guida introduttiva all&#39;API [!DNL Observability Insights]

L&#39;API [!DNL Observability Insights] consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all&#39;API [!DNL Observability Insights].

## Lettura delle chiamate API di esempio

La documentazione API [!DNL Observability Insights] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su come leggere le chiamate API di esempio nella [guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

## Intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Observability Insights], passare alla [guida dell&#39;endpoint delle metriche](./metrics.md).
