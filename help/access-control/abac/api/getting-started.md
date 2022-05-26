---
keywords: Experience Platform;home;argomenti comuni;controllo degli accessi basato su attributi;controllo degli accessi basato su attributi
title: Guida introduttiva al controllo degli accessi basati su attributi
description: Il controllo dell'accesso basato su attributi consente di gestire in modo programmatico ruoli e criteri in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
hide: true
hidefromtoc: true
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 4%

---

# Guida introduttiva al controllo degli accessi basato sugli attributi

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

Questa guida per sviluppatori descrive i passaggi necessari per utilizzare il controllo degli accessi basato sugli attributi per gestire ruoli, prodotti, categorie di autorizzazioni e set di autorizzazioni in Adobe Experience Platform e include chiamate API di esempio per l’esecuzione di varie operazioni.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulla [come leggere le chiamate API di esempio](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Raccogli i valori delle intestazioni richieste

Questa guida richiede il completamento della [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API di Platform. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà effettuata l&#39;operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

## Passaggi successivi

Dopo aver raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui loro endpoint e illustra chiamate API di esempio per l’esecuzione di operazioni CRUD. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.

Per iniziare a effettuare chiamate all’API di controllo accessi basata sugli attributi, consulta le seguenti esercitazioni API:

* [Endpoint ruoli](./roles.md)
* [Endpoint prodotti](./products.md)
