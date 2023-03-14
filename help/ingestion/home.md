---
keywords: Experience Platform;home;argomenti popolari;inserimento dati;posizione dati;posizione dati;gestione dati;gestione dati;derivazione;batch;dati acquisiti;home;popular topic;data ingestion;data location;Data Location;Data management;data management;Lineage;lineage;batch;Batch;ingested data
solution: Experience Platform
title: Panoramica sull’inserimento di dati
description: Questo documento illustra i tre modi principali in cui i dati vengono acquisiti in Platform, con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 15%

---

# Panoramica sull’acquisizione dei dati

Adobe Experience Platform riunisce dati provenienti da più origini per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi con cui [!DNL Platform] acquisisce i dati da queste origini, nonché il modo in cui i dati vengono memorizzati all’interno del Data Lake per l’utilizzo da parte di downstream [!DNL Platform] servizi.

Questo documento introduce i tre modi principali in cui i dati vengono acquisiti in [!DNL Platform], con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.

## Acquisizione batch

L’acquisizione in batch consente di acquisire dati in [!DNL Experience Platform] come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Una volta acquisiti, i batch forniscono i metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come file CSV semplici (mappati a schemi XDM) e dataframe di dati Parquet, devono essere acquisiti con questo metodo.

Consulta la [panoramica dell’acquisizione batch](./batch-ingestion/overview.md) per ulteriori informazioni.

## Acquisizione in streaming

L’acquisizione in streaming ti consente di inviare dati da dispositivi lato client e lato server a [!DNL Experience Platform] in tempo reale. [!DNL Platform] supporta l’utilizzo di ingressi di dati per lo streaming dei dati di esperienza in arrivo, che viene mantenuto in set di dati abilitati per lo streaming all’interno del Data Lake. Gli ingressi dati possono essere configurati in modo da autenticare automaticamente i dati raccolti, garantendo che i dati provengano da una sorgente affidabile.

Consulta la [panoramica sull’acquisizione in streaming](./streaming-ingestion/overview.md) per ulteriori informazioni.

## Origini

[!DNL Experience Platform] consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l’autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell’acquisizione e gestire la velocità effettiva di acquisizione.

Le connessioni di origini possono essere configurate per raccogliere dati da altre applicazioni Adobe (come Adobe Analytics e Adobe Audience Manager) e da origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon] S3, server FTP e server SFTP) e sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Consulta la [Panoramica sulle origini](../sources/home.md) per ulteriori informazioni.

## Passaggi successivi e risorse aggiuntive

Questo documento fornisce una breve introduzione ai diversi aspetti di [!DNL Data Ingestion] in [!DNL Experience Platform]. Continua a leggere la documentazione panoramica di ciascun metodo di acquisizione per acquisire familiarità con le diverse funzionalità, i casi di utilizzo e le best practice. Puoi anche integrare le tue conoscenze guardando il video introduttivo sull’acquisizione di seguito. Per informazioni su come [!DNL Experience Platform] tiene traccia dei metadati per i record acquisiti, consulta la sezione [Panoramica di Catalog Service](../catalog/home.md).

>[!WARNING]
>
>Il termine &quot;Profilo unificato&quot; utilizzato nel video seguente è obsoleto. I termini [!DNL "Profile"] o [!DNL "Real-Time Customer Profile"] sono i termini corretti utilizzati nel [!DNL Experience Platform] documentazione. Per informazioni sulle funzionalità più recenti, consulta la documentazione.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
