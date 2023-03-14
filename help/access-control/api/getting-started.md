---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;api;guida introduttiva
solution: Experience Platform
title: Guida API per il controllo degli accessi
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per varie funzionalità di Platform utilizzando Adobe Admin Console. Le sezioni seguenti forniscono informazioni aggiuntive che gli sviluppatori dovranno conoscere per effettuare correttamente chiamate all’API Schema Registry.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# Guida dell’API di [!DNL Access Control]

[!DNL Access control] per [!DNL Experience Platform] viene somministrato tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Consulta la [panoramica sul controllo degli accessi](../home.md) per ulteriori informazioni.

Questa guida per sviluppatori fornisce informazioni su come formattare le richieste per [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/), e riguarda le seguenti operazioni:

- [Elenca i nomi delle autorizzazioni e dei tipi di risorse](./permissions-and-resource-types.md)
- [Visualizza criteri di accesso effettivi per l&#39;utente corrente](./effective-policies.md)

## Introduzione

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate al [!DNL Access Control] API.

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Passaggi successivi

Ora che hai raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per sviluppatori. Ogni sezione fornisce informazioni importanti sugli endpoint e illustra esempi di chiamate API per l’esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente, e una risposta di esempio per una chiamata di successo.
