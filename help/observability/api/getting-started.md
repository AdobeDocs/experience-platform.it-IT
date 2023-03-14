---
keywords: Experience Platform;home;argomenti popolari;intervallo date
solution: Experience Platform
title: Guida introduttiva all’API Observability Insights
description: L’API Observability Insights consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Observability Insights] API

Il [!DNL Observability Insights] API consente di recuperare i dati delle metriche per varie funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Observability Insights] API.

## Lettura delle chiamate API di esempio

Il [!DNL Observability Insights] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su come leggere chiamate API di esempio in [Guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

## Intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Observability Insights] API, passare alla [guida dell’endpoint &quot;metrics&quot;](./metrics.md).
