---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Guida introduttiva all’API del servizio criteri
topic-legacy: developer guide
description: L’API del servizio criteri consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API del servizio criteri.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Guida introduttiva all’ API [!DNL Policy Service]

L’ API [!DNL Policy Service] ti consente di creare e gestire varie risorse correlate a Adobe Experience Platform [!DNL Data Governance]. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’ API [!DNL Policy Service] .

## Prerequisiti

L’utilizzo della guida per gli sviluppatori richiede una buona comprensione dei vari servizi [!DNL Experience Platform] coinvolti nell’utilizzo delle funzionalità di governance dei dati. Prima di iniziare a lavorare con [!DNL Policy Service API], controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Data Governance]](../home.md): Il framework in base al quale  [!DNL Experience Platform] viene applicata la conformità per l’utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Lettura di chiamate API di esempio

La documentazione [!DNL Policy Service] API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform], comprese quelle appartenenti a [!DNL Data Governance], sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Core e risorse personalizzate

All’interno dell’API [!DNL Policy Service], tutti i criteri e le azioni di marketing sono definiti risorse `core` o `custom`.

`core` le risorse sono quelle definite e gestite dall’Adobe, mentre  `custom` le risorse sono quelle create e gestite dall’organizzazione e sono quindi uniche e visibili solo all’organizzazione IMS. Le operazioni di elenco e ricerca (`GET`) sono pertanto le uniche operazioni consentite sulle risorse `core`, mentre le operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH` e `DELETE`) sono disponibili per le risorse `custom`.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API di Policy Service, seleziona una delle guide degli endpoint disponibili.
