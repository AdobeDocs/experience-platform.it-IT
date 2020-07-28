---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori API Sandbox
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Guida per gli sviluppatori API Sandbox

Le sandbox in  Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzionalità, eseguire esperimenti e creare configurazioni personalizzate senza influire sull&#39;ambiente di produzione.

Questa guida per gli sviluppatori fornisce passaggi utili per utilizzare l&#39;API Sandbox per gestire le sandbox in  Experience Platform e include chiamate API di esempio per eseguire varie operazioni.

## Guida introduttiva all&#39;API Sandbox

Per gestire le sandbox per l’organizzazione IMS, è necessario disporre delle autorizzazioni Amministrazione sandbox. Gli utenti senza autorizzazioni di accesso possono utilizzare l&#39;endpoint solo per [elencare le sandbox attive per l&#39;utente](./list-active-sandboxes.md)corrente. Consultate la panoramica [del controllo di](../../access-control/home.md) accesso per ulteriori informazioni su come assegnare le autorizzazioni sandbox per  Experience Platform.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Questa guida richiede che sia stata completata l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate alle API Platform. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un&#39;intestazione che specifica il nome della sandbox in cui si svolgerà l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato **** API generale, una **richiesta** di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una **risposta** di esempio per una chiamata riuscita.