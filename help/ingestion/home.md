---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull’inserimento dei dati in Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Panoramica sull&#39;inserimento dei dati

Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L&#39;inserimento dei dati in Adobe Experience Platform rappresenta i diversi metodi mediante i quali la piattaforma acquisisce i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per essere utilizzati dai servizi della piattaforma a valle.

Questo documento presenta i tre modi principali in cui i dati vengono trasferiti in Piattaforma, con collegamenti alla rispettiva documentazione di panoramica per ottenere informazioni più dettagliate.

## Caricamento batch

L’assimilazione in batch consente di trasferire i dati in Experience Platform come file in batch. I batch sono unità di dati costituite da uno o più file da assimilare come singola unità. Una volta ingeriti, i batch forniscono i metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come file CSV semplici (mappati a schemi XDM) e i fotogrammi di dati Parquet, devono essere acquisiti con questo metodo.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione dei](./batch-ingestion/overview.md) batch.

## Caricamento in streaming

L’assimilazione dello streaming consente di inviare in tempo reale dati da dispositivi lato client e lato server a Experience Platform. Piattaforma supporta l&#39;utilizzo di ingressi di dati per lo streaming di dati di esperienza in arrivo, persistenti nei set di dati abilitati per lo streaming all&#39;interno del Data Lake. È possibile configurare le ingressi dei dati per l&#39;autenticazione automatica dei dati raccolti, garantendo che i dati provengano da un&#39;origine affidabile.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione](./streaming-ingestion/overview.md) in streaming.

## Origini

Experience Platform consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l&#39;autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione.

Le connessioni di origine possono essere configurate per raccogliere dati da altre applicazioni Adobe (come Adobe Analytics e Adobe Audience Manager), origini di archiviazione cloud di terze parti (come Azure Blob, Amazon S3, server FTP e server SFTP) e sistemi CRM di terze parti (come Microsoft Dynamics e Salesforce).

Per ulteriori informazioni, consulta la panoramica [](../source-connectors/home.md) Origini.

## Passaggi successivi

Questo documento ha fornito una breve introduzione ai diversi aspetti dell&#39;inserimento dei dati in Experience Platform. Continua a leggere la documentazione di panoramica di ogni metodo di assimilazione per acquisire dimestichezza con le diverse funzionalità, casi di utilizzo e procedure ottimali. Per informazioni sul modo in cui Experience Platform tiene traccia dei metadati per i record acquisiti, consultate la panoramica [del servizio](../catalog/home.md)catalogo.