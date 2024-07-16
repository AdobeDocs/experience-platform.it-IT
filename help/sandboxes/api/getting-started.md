---
keywords: Experience Platform;home;argomenti popolari;guida per sviluppatori sandbox
solution: Experience Platform
title: Guida introduttiva all’API Sandbox
description: L’API Sandbox consente agli sviluppatori di gestire in modo programmatico le sandbox in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 15%

---

# Guida introduttiva all’API Sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.

Questa guida per gli sviluppatori descrive i passaggi necessari per utilizzare l’API Sandbox per gestire le sandbox in Experience Platform e include esempi di chiamate API per eseguire varie operazioni.

## Prerequisiti

Per gestire le sandbox per la tua organizzazione, devi disporre delle autorizzazioni di amministrazione delle sandbox. Gli utenti senza autorizzazioni di accesso possono utilizzare solo l&#39;[endpoint sandbox disponibile](./available.md) per elencare le sandbox attive per l&#39;utente corrente. Per ulteriori informazioni su come assegnare le autorizzazioni sandbox, ad Experience Platform, consulta la [panoramica sul controllo degli accessi](../../access-control/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogliere i valori per le intestazioni richieste

Questa guida richiede di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per poter effettuare correttamente le chiamate alle API di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.
