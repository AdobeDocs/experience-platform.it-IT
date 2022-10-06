---
keywords: Experience Platform;risoluzione dei problemi;protezioni;linee guida;
title: Guardrail per l’acquisizione dei dati
description: Questo documento fornisce indicazioni sulle protezioni per l’inserimento dei dati in Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: fa0ddc4c0053018d013c14c568ebb2fd231f4bd2
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 1%

---

# Guardrail per l’acquisizione dei dati

Le guardrail sono soglie che forniscono indicazioni sull’utilizzo dei dati e del sistema, sull’ottimizzazione delle prestazioni e sull’eliminazione di errori o risultati imprevisti in Adobe Experience Platform. I guardrail possono fare riferimento all&#39;uso o al consumo di dati e al trattamento in relazione alle autorizzazioni per le licenze.

Questo documento fornisce indicazioni sulle protezioni per l’inserimento dei dati in Adobe Experience Platform.

## Guardrail per l’acquisizione batch

Nella tabella seguente sono illustrate le protezioni da considerare quando si utilizza il [API di acquisizione batch](./batch-ingestion/overview.md) o fonti:

| Tipo di ingestione | Linee guida | Note |
| --- | --- | --- |
| Acquisizione da data lake tramite l’API di acquisizione batch | <ul><li>Puoi acquisire fino a 20 GB di dati all’ora in un data lake utilizzando l’API di acquisizione batch.</li><li>Il numero massimo di file per batch è 1500.</li><li>La dimensione massima del batch è 100 GB.</li><li>Il numero massimo di proprietà o campi per riga è 10000.</li><li>Il numero massimo di batch al minuto per utente è 138.</li></ul> |
| Assimilazione di data lake utilizzando origini batch | <ul><li>È possibile acquisire fino a 200 GB di dati all’ora in un data lake utilizzando origini di acquisizione batch come [!DNL Azure Blob], [!DNL Amazon S3]e [!DNL SFTP].</li><li>Le dimensioni di un batch devono essere comprese tra 256 MB e 100 GB.</li><li>Il numero massimo di file per batch è 1500.</li></ul> | Consulta la sezione [panoramica di origini](../sources/home.md) per un catalogo di origini da utilizzare per l’inserimento dei dati. |
| Acquisizione batch nel profilo | <ul><li>È possibile acquisire fino a 120 GB di dati all’ora.</li><li>La dimensione massima di una classe di record è 100 KB (soft).</li><li>La dimensione massima di una classe ExperienceEvent è 10 KB (soft).</li><li>La dimensione massima di un singolo record è 1 MB.</li></ul> |
| Numero di batch di profili o ExperienceEvent acquisiti al giorno | **Il numero massimo di batch di profili o ExperienceEvent acquisiti al giorno è 90.** Ciò significa che il totale combinato dei batch di Profile ed ExperienceEvent acquisiti ogni giorno non può superare i 90. L’inserimento di batch aggiuntivi influisce sulle prestazioni del sistema. | Questo è un limite morbido. È possibile superare un limite soft, tuttavia, i limiti soft forniscono una linea guida consigliata per le prestazioni del sistema. |

## Guardrail per l’acquisizione in streaming

Nella tabella seguente sono illustrate le protezioni da considerare quando si utilizza il [streaming ingestion API](./streaming-ingestion/overview.md) o sorgenti di streaming:

| Tipo di ingestione | Linee guida | Note |
| --- | --- | --- |
| Acquisizione in streaming | <ul><li>La dimensione massima del record è di 1 MB, con la dimensione consigliata pari a 10 KB.</li><li>Puoi elaborare 20000 richieste al secondo su Profilo in meno di un minuto.</li><li>Puoi elaborare fino a 20000 richieste al secondo per Data Lake in meno di 15 minuti.</li></ul> | Utilizza l’API di acquisizione batch se hai bisogno di un throughput di dati più elevato. |
| Sorgenti di streaming | <ul><li>La dimensione massima del record è di 1 MB, con la dimensione consigliata pari a 10 KB.</li><li>Le origini in streaming supportano da 4000 a 5000 richieste al secondo al momento della creazione di una nuova connessione sorgente. **Nota**: Possono trascorrere fino a 30 minuti prima che i dati in streaming vengano elaborati completamente sul data lake.</li><li>Puoi elaborare da 4000 a 5000 richieste al secondo a data lake. **Nota**: Possono trascorrere fino a 30 minuti prima che i dati in streaming vengano elaborati completamente sul data lake.</li></ul> | Sorgenti di streaming come [!DNL Kafka], [!DNL Azure Event Hubs]e [!DNL Amazon Kinesis] non utilizzare [!DNL Data Collection Core Service] (DCCS) instradare e può avere limiti di throughput diversi. Consulta la sezione [panoramica di origini](../sources/home.md) per un catalogo di origini da utilizzare per l’inserimento dei dati. |

## Passaggi successivi

Vedi la seguente documentazione per maggiori informazioni sulle protezioni dei dati e del trattamento in Experience Platform:

* [Guardrail per dati Profilo cliente in tempo reale](../profile/guardrails.md)
* [Guardrail per i dati del servizio Identity](../identity-service/guardrails.md)
