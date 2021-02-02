---
keywords: ' Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;Catalogo'
solution: Experience Platform
title: Guida per gli sviluppatori di Catalog Service
topic: developer guide
description: Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l'API Catalog. La guida fornisce quindi chiamate API di esempio per eseguire operazioni chiave utilizzando Catalog.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# [!DNL Catalog Service] guida per sviluppatori

[!DNL Catalog Service] è il sistema di record per la posizione dei dati e la linea di dati in Adobe Experience Platform. [!DNL Catalog] funge da archivio di metadati o &quot;catalogo&quot; in cui è possibile trovare informazioni sui dati al loro interno  [!DNL Experience Platform], senza necessità di accedere ai dati stessi. Per ulteriori informazioni, vedere la [[!DNL Catalog] panoramica](../home.md).

Questa guida per gli sviluppatori fornisce i passaggi necessari per iniziare a utilizzare l&#39;API [!DNL Catalog]. La guida fornisce quindi chiamate API di esempio per eseguire operazioni chiave utilizzando [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni all’interno  [!DNL Experience Platform]. Questa guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Experience Platform] coinvolti nella creazione e gestione di queste risorse:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
* [Caricamento](../../ingestion/batch-ingestion/overview.md) batch: Modalità di  [!DNL Experience Platform] acquisizione e memorizzazione dei dati dai file di dati, come CSV e Parquet.
* [Caricamento](../../ingestion/streaming-ingestion/overview.md) streaming: Modalità di  [!DNL Experience Platform] acquisizione e memorizzazione in tempo reale dei dati da dispositivi lato client e lato server.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o avere a disposizione per eseguire correttamente le chiamate all&#39;API [!DNL Catalog Service].

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

* Content-Type: application/json

## Procedure ottimali per le chiamate API [!DNL Catalog]

Quando si eseguono richieste di GET all&#39;API [!DNL Catalog], è consigliabile includere nelle richieste i parametri di query per restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono portare i payload di risposta a oltre 3 GB di dimensione, il che può rallentare le prestazioni complessive.

È possibile visualizzare oggetti specifici includendo il relativo ID nel percorso della richiesta oppure utilizzare parametri di query quali `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Per ulteriori informazioni, consulta il documento sul [filtro dei dati del catalogo](filter-data.md).

Poiché alcune query possono caricare eccessivamente l&#39;API, sono stati implementati limiti globali sulle [!DNL Catalog] query per supportare ulteriormente le procedure ottimali.

## Passaggi successivi

Questo documento ha trattato le conoscenze preliminari necessarie per effettuare chiamate all&#39;API [!DNL Catalog]. Potete ora procedere alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza l&#39;endpoint `/dataSets`, ma i principi possono essere applicati ad altri endpoint all&#39;interno di [!DNL Catalog] (ad esempio `/batches` e `/accounts`). Per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint, vedi [Riferimento API servizio catalogo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Per un flusso di lavoro dettagliato che illustra come l&#39;API [!DNL Catalog] è coinvolta nell&#39;assimilazione dei dati, vedete l&#39;esercitazione su [creazione di un dataset](../datasets/create.md).
