---
solution: Experience Platform
title: Guida introduttiva all’API Unified Tags
description: La seguente documentazione fornisce ulteriori informazioni che è necessario conoscere per lavorare correttamente con l’API Unified Tags.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# Guida introduttiva all’API Unified Tags {#getting-started}

L’API Tag unificati consente di categorizzare e gestire gli oggetti business in Adobe Experience Platform.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per lavorare correttamente con l’API Unified Tags.

## Lettura delle chiamate API di esempio

La documentazione API per tag unificati fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull&#39;utilizzo delle sandbox in [!DNL Experience Platform], consulta la [documentazione panoramica sulle sandbox](../../sandboxes/home.md).

## Passaggi successivi

Per effettuare chiamate utilizzando l&#39;API Unified Tags, seleziona una delle guide endpoint disponibili utilizzando la barra di navigazione a sinistra o nella [panoramica della guida per sviluppatori](./overview.md)
