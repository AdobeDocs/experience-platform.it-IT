---
solution: Experience Platform
title: Guida introduttiva all’API Unified Tags
description: La seguente documentazione fornisce ulteriori informazioni che è necessario conoscere per lavorare correttamente con l’API Unified Tags.
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# Guida introduttiva all’API Unified Tags {#getting-started}

L’API Tag unificati consente di categorizzare e gestire gli oggetti business in Adobe Experience Platform.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per lavorare correttamente con l’API Unified Tags.

## Lettura delle chiamate API di esempio

La documentazione API per tag unificati fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente chiamate agli endpoint di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experienci Platform, come mostrato di seguito:

- Autorizzazione `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in [!DNL Experience Platform], vedere [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando l’API Unified Tags, seleziona una delle guide endpoint disponibili utilizzando la barra di navigazione a sinistra o all’interno di [panoramica della guida per sviluppatori](./overview.md)
