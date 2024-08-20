---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;posizione dati;posizione dati;gestione dati;gestione dati;derivazione;batch;dati acquisiti;home;popular topic;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Panoramica sull’acquisizione dei dati
description: Questo documento illustra i tre modi principali in cui i dati vengono acquisiti in Platform, con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 3%

---

# Panoramica sull’acquisizione dei dati

Adobe Experience Platform riunisce dati provenienti da più origini per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi con cui Experience Platform acquisisce i dati da queste origini, nonché il modo in cui tali dati vengono mantenuti all’interno del Data Lake per l’utilizzo da parte dei servizi di Experience Platform a valle.

Questo documento illustra i tre modi principali in cui i dati vengono acquisiti in Experience Platform, con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.

## Acquisizione in batch

L&#39;acquisizione in batch consente di acquisire dati in [!DNL Experience Platform] come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Una volta acquisiti, i batch forniscono metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come file CSV semplici (mappati a schemi XDM) e dataframe di dati Parquet, devono essere acquisiti con questo metodo.

Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione batch](./batch-ingestion/overview.md).

>[!TIP]
>
>Utilizza il JSON a riga singola invece del JSON su più righe come input per l’acquisizione batch. Il formato JSON a riga singola consente prestazioni migliori in quanto il sistema può dividere un file di input in più blocchi ed elaborarli in parallelo, mentre il formato JSON a riga multipla non può essere diviso. Ciò può ridurre in modo significativo i costi di elaborazione dei dati e migliorare la latenza dell’elaborazione batch.

## Acquisizione in streaming

L&#39;acquisizione in streaming ti consente di inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform]. Experience Platform supporta l’utilizzo di ingressi di dati per lo streaming dei dati di esperienza in arrivo, che viene mantenuto in set di dati abilitati per lo streaming all’interno del Data Lake. Gli ingressi dati possono essere configurati in modo da autenticare automaticamente i dati raccolti, garantendo che i dati provengano da una sorgente affidabile.

Per ulteriori informazioni, consulta la [panoramica sull&#39;acquisizione in streaming](./streaming-ingestion/overview.md).

## Origini

[!DNL Experience Platform] consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l’autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell’acquisizione e gestire la velocità effettiva di acquisizione.

Le connessioni Source possono essere configurate per raccogliere dati da altre applicazioni Adobe (come Adobe Analytics e Adobe Audience Manager), da origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon] S3, server FTP e server SFTP) e da sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Per ulteriori informazioni, vedere [Panoramica origini](../sources/home.md).

### Creazione di schemi con assistenza ML {#ml-assisted-schema-creation}

Per integrare rapidamente nuove origini dati, ora puoi utilizzare algoritmi di apprendimento automatico per generare uno schema dai dati di esempio. Questa automazione semplifica la creazione di schemi accurati, riduce gli errori e velocizza il processo dalla raccolta dei dati all’analisi e alle informazioni.

Per ulteriori informazioni su questo flusso di lavoro, consulta la [Guida alla creazione di schemi assistiti da ML](../xdm/ui/ml-assisted-schema-creation.md).

## Passaggi successivi e risorse aggiuntive

Questo documento fornisce una breve introduzione ai diversi aspetti di [!DNL Data Ingestion] in [!DNL Experience Platform]. Continua a leggere la documentazione panoramica di ciascun metodo di acquisizione per acquisire familiarità con le diverse funzionalità, i casi di utilizzo e le best practice. Puoi anche integrare le tue conoscenze guardando il video introduttivo sull’acquisizione di seguito. Per informazioni su come [!DNL Experience Platform] tiene traccia dei metadati per i record acquisiti, consulta la [panoramica di Catalog Service](../catalog/home.md).

>[!WARNING]
>
>Il termine &quot;Profilo unificato&quot; utilizzato nel video seguente è obsoleto. I termini [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] sono i termini corretti utilizzati nella documentazione di [!DNL Experience Platform]. Per informazioni sulle funzionalità più recenti, consulta la documentazione.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
