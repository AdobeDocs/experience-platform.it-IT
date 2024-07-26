---
title: Guida introduttiva all’API del servizio MTLS
description: Questo documento fornisce informazioni aggiuntive che è necessario conoscere per lavorare correttamente con l’API MTLS.
role: Developer
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 7%

---

# Guida introduttiva all’API del servizio MTLS {#getting-started}

L’API del servizio MTLS consente di recuperare e verificare in modo sicuro i certificati pubblici rilasciati da Adobe.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per utilizzare correttamente l’API del servizio MTLS.

## Lettura delle chiamate API di esempio

La documentazione API del servizio MTLS fornisce un esempio di chiamata API per dimostrare come formattare le richieste. Ciò include il percorso, le intestazioni richieste e il payload della richiesta formattato correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di Experience Platform.

## Intestazioni richieste

La documentazione API richiede inoltre di aver completato l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en) per effettuare correttamente le chiamate agli endpoint di Platform. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

## Passaggi successivi

Per effettuare chiamate tramite l&#39;API del servizio MTLS, seleziona le guide dell&#39;endpoint utilizzando la navigazione a sinistra o nella [panoramica della guida per sviluppatori](./overview.md)
