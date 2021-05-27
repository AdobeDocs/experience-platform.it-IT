---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Guida all’API per sandbox
topic-legacy: developer guide
description: L’API Sandbox consente agli sviluppatori di gestire in modo programmatico le sandbox in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# Guida all’API per sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.

Questa guida per gli sviluppatori descrive i passaggi necessari per utilizzare l’API Sandbox per gestire le sandbox in Experience Platform e include chiamate API di esempio per eseguire varie operazioni.

## Guida introduttiva all’API Sandbox

Per gestire le sandbox per l’organizzazione IMS, è necessario disporre delle autorizzazioni di amministrazione sandbox. Gli utenti senza autorizzazioni di accesso possono utilizzare solo l’ [endpoint sandbox disponibili](./available.md) per elencare le sandbox attive per l’utente corrente. Per ulteriori informazioni, ad Experience Platform, su come assegnare le autorizzazioni sandbox, consulta la [panoramica sul controllo degli accessi](../../access-control/home.md) .

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Questa guida richiede di aver completato l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API di Platform. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà effettuata l&#39;operazione:

* nome x-sandbox: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Passaggi successivi

Dopo aver raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui loro endpoint e illustra chiamate API di esempio per l’esecuzione di operazioni CRUD. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
