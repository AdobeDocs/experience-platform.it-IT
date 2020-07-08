---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per lo sviluppatore del controllo degli accessi
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 1%

---


# Guida per lo sviluppatore del controllo degli accessi

Il controllo degli accessi per  Experience Platform è gestito tramite [Adobe  Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in  Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Per ulteriori informazioni, consulta la panoramica [sul controllo](../home.md) degli accessi.

Questa guida per gli sviluppatori fornisce informazioni su come formattare le richieste nell’API [di controllo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)degli accessi e descrive le operazioni seguenti:

- [Nomi elenco di autorizzazioni e tipi di risorse](./permissions-and-resource-types.md)
- [Visualizza criteri effettivi per l&#39;utente corrente](./effective-policies.md)

## Introduzione

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente chiamate all&#39;API del Registro di sistema dello schema.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato **** API generale, una **richiesta** di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una **risposta** di esempio per una chiamata riuscita.