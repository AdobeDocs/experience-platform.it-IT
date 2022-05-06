---
keywords: Experience Platform;home;argomenti comuni;controllo accessi;api;guida introduttiva
solution: Experience Platform
title: Guida all’API di controllo degli accessi
topic-legacy: developer guide
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per varie funzionalità di Platform utilizzando Adobe Admin Console. Le sezioni seguenti forniscono informazioni aggiuntive che gli sviluppatori dovranno conoscere per effettuare correttamente le chiamate all’API del Registro di sistema dello schema.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# Guida dell’API di [!DNL Access Control]

[!DNL Access control] per [!DNL Experience Platform] viene amministrato tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Consulta la sezione [panoramica sul controllo degli accessi](../home.md) per ulteriori informazioni.

Questa guida per gli sviluppatori fornisce informazioni su come formattare le richieste nel [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)e riguarda le seguenti operazioni:

- [Elencare nomi di autorizzazioni e tipi di risorse](./permissions-and-resource-types.md)
- [Visualizza criteri efficaci per l&#39;utente corrente](./effective-policies.md)

## Introduzione

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate al [!DNL Access Control] API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Passaggi successivi

Dopo aver raccolto le credenziali richieste, puoi continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui loro endpoint e illustra chiamate API di esempio per l’esecuzione di operazioni CRUD. Ciascuna chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
