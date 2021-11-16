---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
solution: Experience Platform
title: Guida introduttiva all'SDK per sorgenti (Beta)
topic-legacy: developer guide
description: Questo documento fornisce un’introduzione alle informazioni sui prerequisiti che è necessario conoscere prima di tentare di creare una nuova origine utilizzando l’SDK di Origini.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Guida introduttiva all&#39;SDK per sorgenti (Beta)

>[!IMPORTANT]
>
>L&#39;SDK di Origini è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità descritta in questa documentazione è soggetta a modifiche.

L’SDK per sorgenti consente di integrare la propria origine basata su REST per portare i dati in Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prerequisiti

Per utilizzare l’SDK per sorgenti, devi assicurarti di avere accesso a una sandbox organizzazione IMS con provisioning di origini Adobe Experience Platform.

Questa guida richiede anche una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Sandbox](../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Lettura di chiamate API di esempio

L&#39;SDK per le sorgenti e [!DNL Flow Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in Platform, comprese quelle appartenenti a [!DNL Flow Service], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la sezione [documentazione sandbox](../../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Per iniziare a creare una nuova origine con l’SDK di Origini, consulta l’esercitazione su [creazione di una nuova origine](./create.md).