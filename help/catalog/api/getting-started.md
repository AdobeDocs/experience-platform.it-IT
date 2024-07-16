---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;Catalog service;Catalog
solution: Experience Platform
title: Guida API di Catalog Service
description: L’API Catalog Service consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 25%

---

# Guida dell’API di [!DNL Catalog Service]

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. [!DNL Catalog] funge da archivio o &quot;catalogo&quot; di metadati in cui è possibile trovare informazioni sui dati in [!DNL Experience Platform], senza dover accedere ai dati stessi. Per ulteriori informazioni, vedere [[!DNL Catalog] panoramica](../home.md).

Questa guida per sviluppatori descrive i passaggi per iniziare a utilizzare l’API di [!DNL Catalog]. La guida fornisce quindi esempi di chiamate API per eseguire operazioni chiave utilizzando [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni in [!DNL Experience Platform]. Questa guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nella creazione e gestione di queste risorse:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.
* [Acquisizione in batch](../../ingestion/batch-ingestion/overview.md): in che modo [!DNL Experience Platform] acquisisce e memorizza i dati dai file di dati, ad esempio CSV e Parquet.
* [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): in che modo [!DNL Experience Platform] acquisisce e archivia dati da dispositivi lato client e lato server in tempo reale.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere o avere a disposizione per effettuare correttamente chiamate all&#39;API [!DNL Catalog Service].

## Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Best practice per le chiamate API [!DNL Catalog]

Quando si eseguono richieste di GET all&#39;API [!DNL Catalog], è consigliabile includere parametri di query nelle richieste in modo da restituire solo gli oggetti e le proprietà necessarie. Le richieste non filtrate possono causare payload di risposta di dimensioni superiori a 3 GB, rallentando le prestazioni complessive.

È possibile visualizzare oggetti specifici includendo il relativo ID nel percorso della richiesta oppure utilizzare parametri di query come `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Per ulteriori informazioni, vedere il documento relativo al filtro dei dati del catalogo [1.](filter-data.md)

Poiché alcune query possono comportare un carico pesante sull&#39;API, sono stati implementati limiti globali sulle query [!DNL Catalog] per supportare ulteriormente le best practice.

## Passaggi successivi

Questo documento tratta le conoscenze preliminari necessarie per effettuare chiamate alle API di [!DNL Catalog]. Ora puoi passare alle chiamate di esempio fornite in questa guida per sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza l&#39;endpoint `/dataSets`, ma i principi possono essere applicati ad altri endpoint in [!DNL Catalog] (ad esempio `/batches`). Per un elenco completo di tutte le chiamate e operazioni disponibili per ogni endpoint, vedere il [riferimento API di Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/).

Per un flusso di lavoro dettagliato che illustra il modo in cui l&#39;API [!DNL Catalog] è coinvolta nell&#39;acquisizione dei dati, vedere l&#39;esercitazione sulla [creazione di un set di dati](../datasets/create.md).
