---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Guida introduttiva all’API del servizio criteri
topic-legacy: developer guide
description: L’API del servizio criteri consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API del servizio criteri.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Guida introduttiva a [!DNL Policy Service] API

La [!DNL Policy Service] L’API ti consente di creare e gestire varie risorse relative alla governance dei dati di Adobe Experience Platform. Questo documento fornisce un&#39;introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate al [!DNL Policy Service] API.

## Prerequisiti

L’utilizzo della guida per gli sviluppatori richiede una buona comprensione dei diversi [!DNL Experience Platform] servizi coinvolti nell’utilizzo delle funzionalità di governance dei dati. Prima di iniziare a lavorare con [!DNL Policy Service API], consulta la documentazione relativa ai seguenti servizi:

* [Governance dei dati](../home.md): Il quadro [!DNL Experience Platform] applica la conformità per l’utilizzo dei dati.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Lettura di chiamate API di esempio

La [!DNL Policy Service] La documentazione API fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede anche di aver completato la [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] endpoint. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le risorse in [!DNL Experience Platform], compresi quelli appartenenti alla governance dei dati, sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Core e risorse personalizzate

All&#39;interno di [!DNL Policy Service] API, tutti i criteri e le azioni di marketing sono denominati `core` o `custom` risorse.

`core` le risorse sono quelle definite e gestite dall&#39;Adobe, mentre `custom` Le risorse sono quelle create e gestite dalla tua organizzazione e sono quindi uniche e visibili solo per la tua organizzazione IMS. Di conseguenza, operazioni di inserimento nell’elenco e ricerca (`GET`) sono le uniche operazioni consentite su `core` risorse, mentre operazioni di elenco, ricerca e aggiornamento (`POST`, `PUT`, `PATCH`e `DELETE`) sono disponibili per `custom` risorse.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API di Policy Service, seleziona una delle guide degli endpoint disponibili.
