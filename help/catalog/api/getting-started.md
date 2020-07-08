---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Guida per gli sviluppatori di Catalog Service

Catalog Service è il sistema di record per la posizione dei dati e la linea di dati all&#39;interno  Adobe Experience Platform. Il catalogo funge da archivio di metadati o da &quot;catalogo&quot; in cui è possibile trovare informazioni sui dati in  Experience Platform, senza dover accedere ai dati stessi. Per ulteriori informazioni, consultate la panoramica [del](../home.md) catalogo.

Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l&#39;API Catalog. La guida fornisce quindi chiamate API di esempio per eseguire operazioni chiave utilizzando Catalog.

## Prerequisiti

Catalog tiene traccia dei metadati per diversi tipi di risorse e operazioni all’interno  Experience Platform. Questa guida per gli sviluppatori richiede una conoscenza approfondita dei diversi servizi Experience Platform  relativi alla creazione e alla gestione di tali risorse:

* [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
* [Caricamento](../../ingestion/batch-ingestion/overview.md)batch:  Experience Platform acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
* [Caricamento](../../ingestion/streaming-ingestion/overview.md)streaming:  Experience Platform archivia e archivia i dati da dispositivi lato client e lato server in tempo reale.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39;API del servizio catalogo.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi di  Experience Platform.

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle API Platform, è prima necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte  chiamate API Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in  Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API Platform richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Procedure ottimali per le chiamate API Catalog

Quando si eseguono richieste GET all&#39;API Catalog, è consigliabile includere nelle richieste i parametri di query per restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono portare i payload di risposta a oltre 3 GB di dimensione, il che può rallentare le prestazioni complessive.

È possibile visualizzare oggetti specifici includendo il relativo ID nel percorso della richiesta o utilizzare parametri di query quali `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Per ulteriori informazioni, consulta il documento sul [filtro dei dati](filter-data.md) del catalogo.

Poiché alcune query possono causare un notevole carico sulle API, sono stati implementati limiti globali sulle query Catalog per supportare ulteriormente le procedure ottimali.

## Passaggi successivi

In questo documento sono state descritte le conoscenze preliminari necessarie per effettuare chiamate all&#39;API Catalog. Potete ora procedere alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza l’ `/dataSets` endpoint, ma i principi possono essere applicati ad altri endpoint all’interno di Catalog (ad esempio `/batches` e `/accounts`). Consultate il riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint.

Per un flusso di lavoro dettagliato che illustra come l’API Catalog è coinvolta nell’assimilazione dei dati, consultate l’esercitazione sulla [creazione di un set di dati](../datasets/create.md).
