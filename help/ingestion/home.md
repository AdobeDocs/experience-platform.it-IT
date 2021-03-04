---
keywords: Experience Platform;home;argomenti comuni;inserimento dati;posizione dati;posizione dati;gestione dati;gestione dati;gestione dati;linea;linea;linea;batch;batch;dati acquisiti
solution: Experience Platform
title: Panoramica sull’acquisizione dei dati
topic: ' - Panoramica'
description: Questo documento presenta i tre modi principali in cui i dati vengono acquisiti in Platform, con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 9%

---


# Panoramica sull’acquisizione dei dati

Adobe Experience Platform riunisce dati provenienti da più sorgenti per aiutare gli esperti di marketing a comprendere meglio il comportamento dei loro clienti. L’acquisizione dei dati in Adobe Experience Platform rappresenta i diversi metodi con cui [!DNL Platform] acquisisce i dati da queste sorgenti, nonché il modo in cui tali dati vengono mantenuti all’interno del Data Lake e possono essere utilizzati dai servizi a valle [!DNL Platform].

Questo documento introduce i tre modi principali in cui i dati vengono acquisiti in [!DNL Platform], con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.

## Acquisizione batch

L’acquisizione in batch consente di acquisire dati in [!DNL Experience Platform] come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Una volta acquisiti, i batch forniscono i metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come file CSV semplici (mappati a schemi XDM) e dataframe di dati Parquet, devono essere acquisiti con questo metodo.

Per ulteriori informazioni, consulta la [panoramica sull’acquisizione batch](./batch-ingestion/overview.md) .

## Acquisizione in streaming

L’acquisizione in streaming ti consente di inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform] . [!DNL Platform] supporta l’utilizzo di ingressi di dati per lo streaming dei dati esperienza in arrivo, che viene mantenuto nei set di dati abilitati per lo streaming all’interno del Data Lake. È possibile configurare le ingressi di dati per l’autenticazione automatica dei dati raccolti, in modo che i dati provengano da un’origine affidabile.

Per ulteriori informazioni, consulta la [panoramica sull’acquisizione in streaming](./streaming-ingestion/overview.md) .

## Origini

[!DNL Experience Platform] consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l’autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di acquisizione.

Le connessioni sorgente possono essere configurate per raccogliere dati da altre applicazioni Adobe (come Adobe Analytics e Adobe Audience Manager), origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon] S3, server FTP e server SFTP) e sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Per ulteriori informazioni, consulta la [Panoramica delle sorgenti](../sources/home.md) .

## Passaggi successivi e risorse aggiuntive

Questo documento fornisce una breve introduzione ai diversi aspetti di [!DNL Data Ingestion] in [!DNL Experience Platform]. Continua a leggere la documentazione di panoramica per ogni metodo di acquisizione per acquisire familiarità con le diverse funzionalità, i casi d’uso e le best practice. Puoi anche completare l’apprendimento guardando il video di panoramica sull’acquisizione riportato di seguito. Per informazioni su come [!DNL Experience Platform] tiene traccia dei metadati per i record acquisiti, consulta la [Panoramica del servizio catalogo](../catalog/home.md).

>[!WARNING]
>
>Il termine &quot;Profilo unificato&quot; utilizzato nel video seguente è obsoleto. I termini [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] sono i termini corretti utilizzati nella documentazione [!DNL Experience Platform]. Consulta la documentazione per le funzionalità più recenti.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)