---
keywords: Experience Platform;home;argomenti popolari;guida per gli sviluppatori sandbox
solution: Experience Platform
title: Guida introduttiva all’API Sandbox
description: L’API Sandbox consente agli sviluppatori di gestire in modo programmatico le sandbox in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 5%

---

# Guida introduttiva all’API Sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sull’ambiente di produzione.

Questa guida per gli sviluppatori descrive i passaggi necessari per utilizzare l’API Sandbox per gestire le sandbox in Experience Platform e include chiamate API di esempio per eseguire varie operazioni.

## Prerequisiti

Per gestire le sandbox per l’organizzazione IMS, è necessario disporre delle autorizzazioni di amministrazione sandbox. Gli utenti senza autorizzazioni di accesso possono utilizzare solo le [endpoint sandbox disponibili](./available.md) per elencare le sandbox attive per l’utente corrente. Consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home.md) per ulteriori informazioni su come assegnare le autorizzazioni sandbox, ad Experience Platform.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulla [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

### Raccogli i valori delle intestazioni richieste

Questa guida richiede il completamento della [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate alle API di Platform. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà effettuata l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Passaggi successivi

Dopo aver raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui loro endpoint e illustra chiamate API di esempio per l’esecuzione di operazioni CRUD. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
