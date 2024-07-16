---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
solution: Experience Platform
title: Guida introduttiva alle origini self-service (SDK batch)
description: Questo documento fornisce un’introduzione alle informazioni sui prerequisiti da conoscere prima di tentare di creare una nuova origine utilizzando Origini self-service (SDK batch).
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 17%

---

# Guida introduttiva alle origini self-service (SDK batch)

Origini self-service (SDK batch) consente di integrare una sorgente basata su REST per portare dati batch a Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all&#39;[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prerequisiti

Per utilizzare Origini self-service (SDK batch), è necessario assicurarsi di avere accesso a una sandbox dell’organizzazione fornita con Origini Adobe Experience Platform.

Questa guida richiede anche una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Lettura delle chiamate API di esempio

La documentazione di Self-Service Sources (Batch SDK) e API [!DNL Flow Service] fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in Platform, incluse quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la [documentazione sulle sandbox](../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Per iniziare a creare una nuova origine con Origini self-service (SDK batch), consulta l&#39;esercitazione su [creazione di una nuova origine](./create.md).
