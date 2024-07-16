---
title: Guida introduttiva all’API degli strumenti sandbox
description: Utilizza l’API per gli strumenti Sandbox per esaminare gli artefatti ed esportare e importare un’istantanea delle configurazioni sandbox tra le sandbox. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 15%

---

# Guida introduttiva all’API per gli strumenti sandbox {#getting-started}

Questa guida per sviluppatori descrive i passaggi necessari per utilizzare l’API degli strumenti sandbox per gestire pacchetti e strumenti in Adobe Experience Platform e include esempi di chiamate API per eseguire varie operazioni.

## Lettura delle chiamate API di esempio {#api-calls}

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Vengono inoltre forniti dati JSON di esempio restituiti alla risposta API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogliere i valori per le intestazioni richieste {#headers}

Questa guida richiede di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per poter effettuare correttamente le chiamate alle API di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi {#next-steps}

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.

Per iniziare a effettuare chiamate all’API per strumenti sandbox, consulta i seguenti tutorial API:

* [Endpoint &quot;packages&quot;](./packages.md)
* [Endpoint &quot;tools&quot;](./tools.md)
