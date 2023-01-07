---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
solution: Experience Platform
title: Guida introduttiva all’API Observability Insights
description: L’API Observability Insights ti consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di Observability Insights .
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Observability Insights] API

La [!DNL Observability Insights] L’API ti consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Observability Insights] API.

## Lettura di chiamate API di esempio

La [!DNL Observability Insights] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su come leggere le chiamate API di esempio nel [Guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

## Intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando [!DNL Observability Insights] API, passa a [guida all’endpoint delle metriche](./metrics.md).
