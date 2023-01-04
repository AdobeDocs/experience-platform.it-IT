---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API di acquisizione dei dati
type: Documentation
description: La guida introduttiva all’acquisizione dei dati API descrive i concetti chiave e le funzionalità di base da conoscere prima di poter iniziare a inserire dati in Experience Platform utilizzando le API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# Guida introduttiva all’API di acquisizione dei dati {#getting-started}

Utilizzando gli endpoint API per l’acquisizione dei dati, puoi eseguire operazioni CRUD di base per l’acquisizione dei dati in Adobe Experience Platform.

L’utilizzo delle guide API richiede una buona conoscenza di più servizi Adobe Experience Platform coinvolti nell’utilizzo dei dati. Prima di utilizzare l’API di acquisizione dati, consulta la documentazione relativa ai seguenti servizi:

* [Acquisizione batch](./overview.md): Consente di acquisire dati in Adobe Experience Platform come file batch.
* [[!DNL Real-Time Customer Profile]](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che suddividono un singolo [!DNL Platform] in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate a [!DNL Profile] Endpoint API.

## Lettura di chiamate API di esempio

La documentazione API di acquisizione dati fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Intestazioni richieste

La documentazione API richiede anche di aver completato la [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate a [!DNL Platform] endpoint. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un `Content-Type` intestazione. I valori accettati specifici per ogni chiamata sono forniti nei parametri della chiamata .

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).
