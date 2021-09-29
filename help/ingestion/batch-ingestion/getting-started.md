---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Guida introduttiva all’API di acquisizione dei dati
type: Documentation
description: La guida introduttiva all’acquisizione dei dati API descrive i concetti chiave e le funzionalità di base da conoscere prima di poter iniziare a inserire dati in Experience Platform utilizzando le API.
source-git-commit: 19837e820ab3abdaa0bc8569ad78ce51dec1d21e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Guida introduttiva all’API di acquisizione dei dati {#getting-started}

Utilizzando gli endpoint API per l’acquisizione dei dati, puoi eseguire operazioni CRUD di base per l’acquisizione dei dati in Adobe Experience Platform.

L’utilizzo delle guide API richiede una buona conoscenza di più servizi Adobe Experience Platform coinvolti nell’utilizzo dei dati. Prima di utilizzare l’API di acquisizione dati, consulta la documentazione relativa ai seguenti servizi:

* [Acquisizione](./overview.md) batch: Consente di acquisire dati in Adobe Experience Platform come file batch.
* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fornisce sandbox virtuali che suddividono una singola  [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate agli endpoint API [!DNL Profile].

## Lettura di chiamate API di esempio

La documentazione API di acquisizione dati fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint [!DNL Platform]. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API [!DNL Experience Platform], come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un’intestazione `Content-Type`. I valori accettati specifici per ogni chiamata sono forniti nei parametri della chiamata .

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).
