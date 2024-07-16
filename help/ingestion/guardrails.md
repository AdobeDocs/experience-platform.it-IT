---
keywords: Experience Platform;risoluzione dei problemi;guardrail;linee guida;
title: Guardrail per l’acquisizione dei dati
description: Scopri i guardrail per l’acquisizione dei dati in Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 583eb70235174825dd542b95463784638bdef235
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Guardrail per l’acquisizione dei dati

>[!IMPORTANT]
>
>I guardrail per l’acquisizione in batch e in streaming vengono calcolati a livello di organizzazione e non a livello di sandbox. Ciò significa che l’utilizzo dei dati per sandbox è associato al diritto totale all’utilizzo della licenza che corrisponde all’intera organizzazione. Inoltre, l’utilizzo dei dati nelle sandbox di sviluppo è limitato al 10% del totale dei profili. Per ulteriori informazioni sui diritti di utilizzo della licenza, leggere la [guida alle best practice per la gestione dei dati](../landing/license-usage-and-guardrails/data-management-best-practices.md).

I guardrail sono soglie che forniscono indicazioni per l’utilizzo dei dati e del sistema, l’ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all’utilizzo o al consumo di dati e all’elaborazione in relazione alle licenze concesse.

>[!IMPORTANT]
>
>Controlla i diritti di licenza nell&#39;ordine di vendita e la corrispondente [descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi, oltre a questa pagina di guardrail.

Questo documento fornisce indicazioni sui guardrail per l’acquisizione dei dati in Adobe Experience Platform.

## Guardrail per l’acquisizione batch

La tabella seguente illustra i guardrail da considerare quando si utilizza l&#39;API [batch ingestion](./batch-ingestion/overview.md) o le origini:

| Tipo di acquisizione | Linee guida | Note |
| --- | --- | --- |
| Acquisizione del data lake tramite l’API di acquisizione batch | <ul><li>Puoi acquisire fino a 20 GB di dati all’ora nel data lake utilizzando l’API di acquisizione batch.</li><li>Il numero massimo di file per batch è 1500.</li><li>La dimensione massima del batch è di 100 GB.</li><li>È 10000 il numero massimo di proprietà o campi per riga.</li><li>Il numero massimo di batch al minuto per utente è 2000.</li></ul> | |
| Acquisizione del data lake tramite origini batch | <ul><li>È possibile acquisire fino a 200 GB di dati all&#39;ora nel data lake utilizzando origini di acquisizione batch come [!DNL Azure Blob], [!DNL Amazon S3] e [!DNL SFTP].</li><li>La dimensione del batch deve essere compresa tra 256 MB e 100 GB. Questo vale sia per i dati non compressi che per quelli compressi. Quando i dati compressi non sono compressi nel data lake, si applicano queste limitazioni.</li><li>Il numero massimo di file per batch è 1500.</li><li>La dimensione minima di un file o di una cartella è di 1 byte. Non è possibile acquisire cartelle o file di dimensioni pari a 0 byte.</li></ul> | Leggi la [panoramica origini](../sources/home.md) per un catalogo di origini che puoi utilizzare per l&#39;acquisizione dei dati. |
| Acquisizione in batch nel profilo | <ul><li>La dimensione massima di una classe di record è 100 KB (rigido).</li><li>La dimensione massima di una classe ExperienceEvent è 10 KB (rigido).</li></ul> | |
| Numero di batch di profili o ExperienceEvent acquisiti al giorno | **Il numero massimo di batch di profili o ExperienceEvent acquisiti al giorno è 90.** Ciò significa che il totale combinato dei batch di profili ed ExperienceEvent acquisiti ogni giorno non può superare i 90. L&#39;acquisizione di batch aggiuntivi influisce sulle prestazioni del sistema. | Si tratta di un limite non vincolante. È possibile superare un limite non superabile, tuttavia, i limiti non superabili forniscono una linea guida consigliata per le prestazioni del sistema. |

## Guardrail per acquisizione in streaming

Per informazioni sui guardrail per l&#39;acquisizione in streaming, leggi la [panoramica sull&#39;acquisizione in streaming](./streaming-ingestion/overview.md).

## Guardrail per sorgenti in streaming

La tabella seguente illustra i guardrail da considerare quando si utilizzano le sorgenti di streaming:

| Tipo di acquisizione | Linee guida | Note |
| --- | --- | --- |
| Origini di streaming | <ul><li>La dimensione massima del record è 1 MB, con la dimensione consigliata di 10 KB.</li><li>Le origini di streaming supportano tra 4000 e 5000 richieste al secondo durante l’acquisizione nel data lake. Questo vale per entrambe le connessioni di origine appena create, oltre alle connessioni di origine esistenti. **Nota**: l&#39;elaborazione completa dei dati di streaming nel data lake può richiedere fino a 30 minuti.</li><li>Le origini di streaming supportano un massimo di 1500 richieste al secondo durante l’acquisizione dei dati nel profilo o la segmentazione in streaming.</li></ul> | Le origini di streaming come [!DNL Kafka], [!DNL Azure Event Hubs] e [!DNL Amazon Kinesis] non utilizzano la route [!DNL Data Collection Core Service] (DCCS) e possono avere limiti di velocità effettiva diversi. Consulta la [panoramica delle origini](../sources/home.md) per un catalogo delle origini che puoi utilizzare per l&#39;acquisizione dei dati. |

## Passaggi successivi

Consulta la seguente documentazione per ulteriori informazioni su altri guardrail dei servizi Experience Platform, informazioni sulla latenza end-to-end e informazioni sulle licenze dai documenti di descrizione del prodotto Real-Time CDP:

* [Guardrail Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi Experience Platform.
* [Real-time Customer Data Platform (Edizione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
