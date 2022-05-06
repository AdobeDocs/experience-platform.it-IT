---
keywords: Experience Platform;home;argomenti popolari;servizio catalogo;catalogo;servizio catalogo;Catalogo;Catalogo
solution: Experience Platform
title: Guida all’API del servizio catalogo
topic-legacy: developer guide
description: L’API del servizio catalogo consente agli sviluppatori di gestire i metadati del set di dati in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# Guida dell’API di [!DNL Catalog Service]

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in Adobe Experience Platform. [!DNL Catalog] funge da archivio metadati o &quot;catalogo&quot; in cui è possibile trovare informazioni sui dati all&#39;interno di [!DNL Experience Platform], senza dover accedere ai dati stessi. Consulta la sezione [[!DNL Catalog] panoramica](../home.md) per ulteriori informazioni.

Questa guida per gli sviluppatori descrive i passaggi necessari per iniziare a utilizzare [!DNL Catalog] API. La guida fornisce quindi un esempio di chiamate API per eseguire operazioni chiave utilizzando [!DNL Catalog].

## Prerequisiti

[!DNL Catalog] traccia i metadati per diversi tipi di risorse e operazioni all&#39;interno di [!DNL Experience Platform]. Questa guida per gli sviluppatori richiede una comprensione approfondita dei vari [!DNL Experience Platform] servizi relativi alla creazione e alla gestione di tali risorse:

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.
* [Acquisizione batch](../../ingestion/batch-ingestion/overview.md): Come [!DNL Experience Platform] acquisisce e memorizza i dati dai file di dati, come CSV e Parquet.
* [Acquisizione in streaming](../../ingestion/streaming-ingestion/overview.md): Come [!DNL Experience Platform] acquisisce e archivia in tempo reale i dati da dispositivi lato client e lato server.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere o disporre di disponibilità per effettuare correttamente le chiamate al [!DNL Catalog Service] API.

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* Tipo di contenuto: application/json

## Best practice per [!DNL Catalog] Chiamate API

Quando si eseguono richieste di GET a [!DNL Catalog] API, la best practice prevede l’inclusione di parametri di query nelle richieste per restituire solo gli oggetti e le proprietà necessari. Le richieste non filtrate possono causare il raggiungimento da parte dei payload di risposta di dimensioni superiori a 3 GB, il che può rallentare le prestazioni complessive.

Puoi visualizzare oggetti specifici includendo il loro ID nel percorso della richiesta o utilizzare parametri di query come `properties` e `limit` per filtrare le risposte. I filtri possono essere passati come intestazioni e come parametri di query, con quelli passati come parametri di query che hanno la precedenza. Visualizza il documento in [filtraggio dei dati del catalogo](filter-data.md) per ulteriori informazioni.

Poiché alcune query possono caricare notevolmente l’API, sono stati implementati limiti globali su [!DNL Catalog] richieste per supportare ulteriormente le best practice.

## Passaggi successivi

Il presente documento tratta le conoscenze necessarie per effettuare chiamate [!DNL Catalog] API. Ora puoi passare alle chiamate di esempio fornite in questa guida per gli sviluppatori e seguire le relative istruzioni.

La maggior parte degli esempi in questa guida utilizza i `/dataSets` endpoint, ma i principi possono essere applicati ad altri endpoint all&#39;interno di [!DNL Catalog] (quali `/batches` e `/accounts`). Consulta la sezione [Riferimento API del servizio catalogo](https://www.adobe.io/experience-platform-apis/references/catalog/) per un elenco completo di tutte le chiamate e le operazioni disponibili per ciascun endpoint.

Per un flusso di lavoro dettagliato che mostra come [!DNL Catalog] L’API è coinvolta nell’acquisizione dei dati, consulta l’esercitazione su [creazione di un set di dati](../datasets/create.md).
