---
keywords: ' Experience Platform;home;argomenti popolari;guida per lo sviluppo di sandbox'
solution: Experience Platform
title: Guida API per sandbox
topic: developer guide
description: L'API Sandbox consente agli sviluppatori di gestire in modo programmatico le sandbox in Adobe Experience Platform. Seguite questa guida per apprendere come eseguire operazioni chiave tramite l'API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Guida API sandbox

Le sandbox in Adobe Experience Platform forniscono ambienti di sviluppo isolati che consentono di testare le funzionalità, eseguire esperimenti e creare configurazioni personalizzate senza influire sull&#39;ambiente di produzione.

Questa guida per gli sviluppatori fornisce passaggi utili per utilizzare l&#39;API Sandbox per gestire le sandbox in  Experience Platform e include chiamate API di esempio per eseguire varie operazioni.

## Guida introduttiva all&#39;API Sandbox

Per gestire le sandbox per l’organizzazione IMS, è necessario disporre delle autorizzazioni Amministrazione sandbox. Gli utenti senza autorizzazioni di accesso possono utilizzare l&#39;endpoint solo per [elencare le sandbox attive per l&#39;utente corrente](./list-active-sandboxes.md). Per ulteriori informazioni sull&#39;assegnazione delle autorizzazioni sandbox per  Experience Platform, consultate la [panoramica sul controllo degli accessi](../../access-control/home.md).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi del Experience Platform .

### Raccogli valori per le intestazioni richieste

Per effettuare correttamente le chiamate alle API della piattaforma, questa guida richiede che sia stata completata l&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Oltre alle intestazioni di autenticazione, tutte le richieste richiedono un&#39;intestazione che specifica il nome della sandbox in cui si svolgerà l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Tutte le richieste che contengono un payload (POST, PUT e PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.