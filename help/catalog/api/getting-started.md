---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# [!DNL Catalog Service] guida per sviluppatori

[!DNL Catalog Service] è il sistema di record per la posizione dei dati e la linea all&#39;interno  Adobe Experience Platform. [!DNL Catalog] funge da archivio di metadati o &quot;catalogo&quot; in cui è possibile trovare informazioni sui dati al loro interno [!DNL Experience Platform], senza necessità di accedere ai dati stessi. Per ulteriori informazioni, consultate la panoramica [del](../home.md) catalogo.

Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l&#39; [!DNL Catalog] API. La guida fornisce quindi chiamate API di esempio per eseguire operazioni chiave utilizzando [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni all’interno [!DNL Experience Platform]. Questa guida per gli sviluppatori richiede una buona conoscenza dei vari [!DNL Experience Platform] servizi coinvolti nella creazione e gestione di tali risorse:

* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.
* [Caricamento](../../ingestion/batch-ingestion/overview.md)batch: Modalità di [!DNL Experience Platform] acquisizione e memorizzazione dei dati dai file di dati, come CSV e Parquet.
* [Caricamento](../../ingestion/streaming-ingestion/overview.md)streaming: Modalità di [!DNL Experience Platform] acquisizione e memorizzazione in tempo reale dei dati da dispositivi lato client e lato server.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39; [!DNL Catalog Service] API.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Procedure ottimali per le chiamate [!DNL Catalog] API

Quando si eseguono richieste GET all&#39; [!DNL Catalog] API, è consigliabile includere parametri di query nelle richieste, in modo da restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono portare i payload di risposta a oltre 3 GB di dimensione, il che può rallentare le prestazioni complessive.

È possibile visualizzare oggetti specifici includendo il relativo ID nel percorso della richiesta o utilizzare parametri di query quali `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Per ulteriori informazioni, consulta il documento sul [filtro dei dati](filter-data.md) del catalogo.

Poiché alcune query possono causare un notevole carico sulle API, sono stati implementati limiti globali sulle [!DNL Catalog] query per supportare ulteriormente le procedure ottimali.

## Passaggi successivi

Questo documento ha trattato le conoscenze preliminari necessarie per effettuare chiamate all&#39; [!DNL Catalog] API. Potete ora procedere alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza l&#39; `/dataSets` endpoint, ma i principi possono essere applicati ad altri endpoint all&#39;interno di [!DNL Catalog] (come `/batches` e `/accounts`). Consultate il riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint.

Per un flusso di lavoro dettagliato che illustra come l&#39; [!DNL Catalog] API è coinvolta nell&#39;assimilazione dei dati, vedete l&#39;esercitazione sulla [creazione di un dataset](../datasets/create.md).
