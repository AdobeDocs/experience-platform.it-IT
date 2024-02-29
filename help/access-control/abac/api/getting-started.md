---
keywords: Experience Platform;home;argomenti comuni;Attribute-Based Access Control;attribute-based access control
title: Guida introduttiva all’API di controllo degli accessi basata su attributi
description: L’API di controllo dell’accesso basato su attributi consente di gestire in modo programmatico i ruoli e i criteri di accesso all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 17%

---

# Guida introduttiva all’API di controllo degli accessi basata su attributi

Questa guida per gli sviluppatori descrive i passaggi necessari per utilizzare l’API di controllo degli accessi basata su attributi per gestire ruoli, prodotti, categorie di autorizzazioni e set di autorizzazioni in Adobe Experience Platform e include esempi di chiamate API per l’esecuzione di varie operazioni.

## Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogliere i valori per le intestazioni richieste

Questa guida richiede di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate alle API di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experienci Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.

Consulta i seguenti tutorial API per iniziare ad effettuare chiamate all’API di controllo degli accessi basata su attributi:

* [Endpoint &quot;Roles&quot;](./roles.md)
* [Endpoint prodotti](./products.md)
