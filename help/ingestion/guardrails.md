---
keywords: Experience Platform;risoluzione dei problemi;guardrail;linee guida;
title: Guardrail per l’acquisizione dei dati
description: Scopri i guardrail per l’acquisizione dei dati in Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: b217dd84d9be630a5097e7179af08619ebc135f8
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 1%

---

# Guardrail per l’acquisizione dei dati

I guardrail sono soglie che forniscono indicazioni per l’utilizzo dei dati e del sistema, l’ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all’utilizzo o al consumo di dati e all’elaborazione in relazione alle licenze concesse.

Questo documento fornisce indicazioni sui guardrail per l’acquisizione dei dati in Adobe Experience Platform.

## Guardrail per l’acquisizione batch

La tabella seguente illustra i guardrail da considerare quando si utilizza [API di acquisizione batch](./batch-ingestion/overview.md) o origini:

| Tipo di acquisizione | Linee guida | Note |
| --- | --- | --- |
| Acquisizione del data lake tramite l’API di acquisizione batch | <ul><li>Puoi acquisire fino a 20 GB di dati all’ora nel data lake utilizzando l’API di acquisizione batch.</li><li>Il numero massimo di file per batch è 1500.</li><li>La dimensione massima del batch è di 100 GB.</li><li>È 10000 il numero massimo di proprietà o campi per riga.</li><li>Il numero massimo di batch al minuto per utente è 138.</li></ul> |
| Acquisizione del data lake tramite origini batch | <ul><li>Puoi acquisire fino a 200 GB di dati all’ora nel data lake utilizzando origini di acquisizione batch come [!DNL Azure Blob], [!DNL Amazon S3], e [!DNL SFTP].</li><li>La dimensione del batch deve essere compresa tra 256 MB e 100 GB. Questo vale sia per i dati non compressi che per quelli compressi. Quando i dati compressi non sono compressi nel data lake, si applicano queste limitazioni.</li><li>Il numero massimo di file per batch è 1500.</li><li>La dimensione minima di un file o di una cartella è di 1 byte. Non è possibile acquisire cartelle o file di dimensioni pari a 0 byte.</li></ul> | Leggi le [panoramica sulle origini](../sources/home.md) per un catalogo di origini che puoi utilizzare per l’acquisizione dei dati. |
| Acquisizione in batch nel profilo | <ul><li>La dimensione massima di una classe di record è 100 KB (soft).</li><li>La dimensione massima di una classe ExperienceEvent è 10 KB (soft).</li><li>La dimensione massima di un singolo record è 1 MB.</li></ul> |
| Numero di batch di profili o ExperienceEvent acquisiti al giorno | **Il numero massimo di batch di profili o ExperienceEvent acquisiti al giorno è 90.** Ciò significa che il totale combinato di batch di profili ed ExperienceEvent acquisiti ogni giorno non può superare i 90. L&#39;acquisizione di batch aggiuntivi influisce sulle prestazioni del sistema. | Si tratta di un limite non vincolante. È possibile superare un limite non superabile, tuttavia, i limiti non superabili forniscono una linea guida consigliata per le prestazioni del sistema. |

## Guardrail per acquisizione in streaming

Leggi le [panoramica sull’acquisizione in streaming](./streaming-ingestion/overview.md) per informazioni sui guardrail per l’acquisizione in streaming.

## Guardrail per sorgenti in streaming

La tabella seguente illustra i guardrail da considerare quando si utilizzano le sorgenti di streaming:

| Tipo di acquisizione | Linee guida | Note |
| --- | --- | --- |
| Origini di streaming | <ul><li>La dimensione massima del record è 1 MB, con la dimensione consigliata di 10 KB.</li><li>Le origini di streaming supportano tra 4000 e 5000 richieste al secondo durante l’acquisizione nel data lake. Questo vale per entrambe le connessioni di origine appena create, oltre alle connessioni di origine esistenti. **Nota**: possono essere necessari fino a 30 minuti affinché i dati in streaming vengano completamente elaborati nel data lake.</li><li>Le origini di streaming supportano un massimo di 1500 richieste al secondo durante l’acquisizione dei dati nel profilo o la segmentazione in streaming.</li></ul> | Origini di streaming come [!DNL Kafka], [!DNL Azure Event Hubs], e [!DNL Amazon Kinesis] non utilizzare il [!DNL Data Collection Core Service] (DCCS) e possono avere diversi limiti di velocità effettiva. Consulta la [panoramica sulle origini](../sources/home.md) per un catalogo di origini che puoi utilizzare per l’acquisizione dei dati. |

## Passaggi successivi

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experienci Platform, informazioni sulla latenza end-to-end e informazioni sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi di Experience Platform.
* [Real-time Customer Data Platform (versione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
