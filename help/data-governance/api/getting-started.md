---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Guida introduttiva all’API del servizio criteri
description: L’API del servizio criteri consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti fondamentali che è necessario conoscere prima di tentare di effettuare chiamate all’API del servizio criteri.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Policy Service] API

Il [!DNL Policy Service] API consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Policy Service] API.

## Prerequisiti

L’utilizzo della guida per sviluppatori richiede una buona conoscenza delle varie [!DNL Experience Platform] servizi coinvolti nell’utilizzo delle funzionalità di governance dei dati. Prima di iniziare a utilizzare [!DNL Policy Service API], consulta la documentazione relativa ai seguenti servizi:

* [Governance dei dati](../home.md): framework tramite il quale [!DNL Experience Platform] applica la conformità all’utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che permettono di suddividere un singolo [!DNL Platform] in ambienti virtuali separati, per facilitare lo sviluppo e l’evoluzione delle applicazioni di esperienza digitale.

## Lettura delle chiamate API di esempio

Il [!DNL Policy Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate a [!DNL Platform] endpoint. Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], inclusi quelli appartenenti alla governance dei dati, sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Risorse core e personalizzate

All&#39;interno del [!DNL Policy Service] API, tutti i criteri e le azioni di marketing sono denominati `core` o `custom` risorse.

`core` le risorse sono quelle definite e mantenute dall&#39;Adobe, mentre `custom` Le risorse sono quelle create e gestite dall’organizzazione e sono quindi uniche e visibili solo all’organizzazione. Di conseguenza, le operazioni di elenco e ricerca (`GET`) sono le uniche operazioni consentite il `core` risorse, mentre le operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH`, e `DELETE`) sono disponibili per `custom` risorse.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API del servizio criteri, seleziona una delle guide degli endpoint disponibili.
