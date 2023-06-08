---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;Catalog service;Catalog
solution: Experience Platform
title: Guida API di Catalog Service
description: L’API Catalog Service consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 07451b8ab4bcb7ca43ad0c8a821478b2c9682894
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 5%

---

# Guida dell’API di [!DNL Catalog Service]

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. [!DNL Catalog] funge da archivio o &quot;catalogo&quot; di metadati in cui è possibile trovare informazioni sui dati all’interno di [!DNL Experience Platform], senza dover accedere ai dati stessi. Consulta la [[!DNL Catalog] panoramica](../home.md) per ulteriori informazioni.

Questa guida per sviluppatori descrive i passaggi per iniziare a utilizzare [!DNL Catalog] API. La guida fornisce quindi esempi di chiamate API per eseguire operazioni chiave tramite [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni in [!DNL Experience Platform]. Questa guida per sviluppatori richiede una buona conoscenza delle varie [!DNL Experience Platform] servizi coinvolti nella creazione e nella gestione di queste risorse:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.
* [Acquisizione in batch](../../ingestion/batch-ingestion/overview.md): Come [!DNL Experience Platform] acquisisce e memorizza dati da file di dati, come CSV e Parquet.
* [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): Come [!DNL Experience Platform] acquisisce e memorizza in tempo reale i dati da dispositivi lato client e lato server.

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere o disporre di per effettuare correttamente chiamate al [!DNL Catalog Service] API.

## Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nel [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Raccogli i valori per le intestazioni richieste

Per effettuare chiamate a [!DNL Platform] , devi prima completare le [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Content-Type: application/json

## Best practice per [!DNL Catalog] Chiamate API

Quando si eseguono richieste di GET a [!DNL Catalog] API, la best practice consiste nell’includere parametri di query nelle richieste per restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono causare payload di risposta di dimensioni superiori a 3 GB, rallentando le prestazioni complessive.

Puoi visualizzare oggetti specifici includendo il loro ID nel percorso della richiesta o utilizzando parametri di query come `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Vedi il documento su [filtraggio dei dati catalogo](filter-data.md) per ulteriori informazioni.

Poiché alcune query possono comportare un carico pesante sull’API, i limiti globali sono stati implementati su [!DNL Catalog] query per supportare ulteriormente le best practice.

## Passaggi successivi

In questo documento sono state trattate le conoscenze preliminari necessarie per effettuare chiamate [!DNL Catalog] API. Ora puoi passare alle chiamate di esempio fornite in questa guida per sviluppatori e seguire le loro istruzioni.

La maggior parte degli esempi contenuti in questa guida utilizza `/dataSets` endpoint, ma i principi possono essere applicati ad altri endpoint all’interno di [!DNL Catalog] (ad esempio `/batches`). Consulta la [Riferimento API di Catalog Service](https://www.adobe.io/experience-platform-apis/references/catalog/) per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint.

Per un flusso di lavoro dettagliato che dimostri come [!DNL Catalog] L’API è coinvolta nell’acquisizione dei dati; consulta l’esercitazione su [creazione di un set di dati](../datasets/create.md).
