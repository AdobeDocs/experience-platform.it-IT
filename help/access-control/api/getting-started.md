---
keywords: ' Experience Platform;home;argomenti popolari;controllo degli accessi;api;guida introduttiva'
solution: Experience Platform
title: Guida per lo sviluppatore del controllo degli accessi
topic: developer guide
description: Il controllo degli accessi in Adobe Experience Platform consente di gestire ruoli e autorizzazioni per diverse funzionalità della piattaforma utilizzando l'Adobe Admin Console. Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente chiamate all'API del Registro di sistema dello schema.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---


# [!DNL Access control] guida per sviluppatori

[!DNL Access control] for  [!DNL Experience Platform] viene amministrato tramite  [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in  Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](../home.md).

Questa guida per gli sviluppatori fornisce informazioni su come formattare le richieste in [[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) e illustra le seguenti operazioni:

- [Nomi elenco di autorizzazioni e tipi di risorse](./permissions-and-resource-types.md)
- [Visualizza criteri effettivi per l&#39;utente corrente](./effective-policies.md)

## Introduzione

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate all&#39;API [!DNL Schema Registry].

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Passaggi successivi

Ora che avete raccolto le credenziali richieste, potete continuare a leggere il resto della guida per gli sviluppatori. Ogni sezione fornisce informazioni importanti sui relativi endpoint e illustra le chiamate API di esempio per l&#39;esecuzione di operazioni CRUD. Ogni chiamata include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e i payload formattati correttamente e una risposta di esempio per una chiamata riuscita.
