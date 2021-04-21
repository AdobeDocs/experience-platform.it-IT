---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
solution: Experience Platform
title: Guida introduttiva all’API Observability Insights
topic-legacy: developer guide
description: L’API Observability Insights ti consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di Observability Insights .
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Guida introduttiva all’ API [!DNL Observability Insights]

L’ [!DNL Observability Insights] API ti consente di recuperare i dati delle metriche per diverse funzioni di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’ API [!DNL Observability Insights] .

## Lettura di chiamate API di esempio

La documentazione [!DNL Observability Insights] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su come leggere le chiamate API di esempio nella [guida alla risoluzione dei problemi di Experience Platform](../../landing/troubleshooting.md).

## Intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione. Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API [!DNL Observability Insights], procedi alla guida dell&#39;endpoint [metriche](./metrics.md).
