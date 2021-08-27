---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;Catalogo;Catalogo
solution: Experience Platform
title: Guida all’API del servizio catalogo
topic-legacy: developer guide
description: L’API del servizio catalogo consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# Guida dell’API di [!DNL Catalog Service]

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. [!DNL Catalog] funge da archivio di metadati o &quot;catalogo&quot; in cui è possibile trovare informazioni sui dati all’interno di  [!DNL Experience Platform], senza dover accedere ai dati stessi. Per ulteriori informazioni, consulta la sezione [[!DNL Catalog] panoramica](../home.md) .

Questa guida per gli sviluppatori descrive i passaggi necessari per iniziare a utilizzare l’ API [!DNL Catalog] . La guida fornisce quindi un esempio di chiamate API per eseguire operazioni chiave utilizzando [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] tiene traccia dei metadati per diversi tipi di risorse e operazioni all’interno di  [!DNL Experience Platform]. Questa guida per gli sviluppatori richiede una buona comprensione dei vari servizi [!DNL Experience Platform] coinvolti nella creazione e gestione di queste risorse:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.
* [Acquisizione](../../ingestion/batch-ingestion/overview.md) batch: Come  [!DNL Experience Platform] acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
* [Acquisizione](../../ingestion/streaming-ingestion/overview.md) in streaming: Come  [!DNL Experience Platform] acquisire e memorizzare in tempo reale i dati da dispositivi lato client e lato server.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere o disporre di a tua disposizione per effettuare correttamente le chiamate all’ API [!DNL Catalog Service] .

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Best practice per le chiamate API [!DNL Catalog]

Quando si eseguono richieste GET all&#39;API [!DNL Catalog], è consigliabile includere nelle richieste i parametri di query al fine di restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono causare il raggiungimento da parte dei payload di risposta di dimensioni superiori a 3 GB, il che può rallentare le prestazioni complessive.

Puoi visualizzare oggetti specifici includendo il loro ID nel percorso della richiesta o utilizzare parametri di query come `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Per ulteriori informazioni, consulta il documento sul [filtraggio dei dati del catalogo](filter-data.md) .

Poiché alcune query possono caricare notevolmente l’API, sono stati implementati limiti globali sulle query [!DNL Catalog] per supportare ulteriormente le best practice.

## Passaggi successivi

Questo documento tratta le conoscenze preliminari necessarie per effettuare chiamate all’ API [!DNL Catalog] . Ora puoi passare alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza l’endpoint `/dataSets`, ma i principi possono essere applicati ad altri endpoint all’interno di [!DNL Catalog] (ad esempio `/batches` e `/accounts`). Per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint, consulta [Riferimento API del servizio catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/) .

Per un flusso di lavoro dettagliato che illustra come l’ [!DNL Catalog] API è coinvolta nell’inserimento dei dati, consulta l’esercitazione su [creazione di un set di dati](../datasets/create.md).
