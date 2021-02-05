---
keywords: ' Experience Platform;home;argomenti popolari;inserimento dati;data location;data Location;Data Management;data management;Lineage;lineage;batch;batch;dati acquisiti'
solution: Experience Platform
title: Panoramica sull'inserimento dei dati
topic: overview
description: Questo documento presenta i tre modi principali in cui i dati vengono trasferiti in Piattaforma, con collegamenti alla rispettiva documentazione di panoramica per ottenere informazioni più dettagliate.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 9%

---


# Panoramica sull&#39;inserimento dei dati

Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli addetti al marketing a comprendere meglio il comportamento dei loro clienti. Adobe Experience Platform Data Ingestion rappresenta i diversi metodi mediante i quali [!DNL Platform] acquisisce i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per essere utilizzati dai servizi a valle [!DNL Platform].

Questo documento introduce i tre modi principali in cui i dati vengono trasferiti in [!DNL Platform], con collegamenti alla rispettiva documentazione di panoramica per ottenere informazioni più dettagliate.

## Caricamento batch

L&#39;assimilazione batch consente di assimilare i dati in [!DNL Experience Platform] come file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Una volta acquisiti, i batch forniscono i metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come i file CSV semplici (mappati a schemi XDM) e i fotogrammi di dati Parquet, devono essere acquisiti con questo metodo.

Per ulteriori informazioni, vedere la [panoramica sull&#39;inserimento dei batch](./batch-ingestion/overview.md).

## Caricamento in streaming

L&#39;assimilazione dello streaming consente di inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform]. [!DNL Platform] supporta l&#39;utilizzo di insenature di dati per lo streaming di dati esperienza in arrivo, persistenti nei set di dati abilitati per lo streaming all&#39;interno del Data Lake. È possibile configurare le ingressi dei dati per l&#39;autenticazione automatica dei dati raccolti, garantendo che i dati provengano da un&#39;origine affidabile.

Per ulteriori informazioni, vedere la [panoramica sull&#39;assimilazione in streaming](./streaming-ingestion/overview.md).

## Origini

[!DNL Experience Platform] consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l&#39;autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione.

Le connessioni di origine possono essere configurate per raccogliere dati da altre applicazioni  Adobe (come  Adobe Analytics e Adobe Audience Manager), origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon] S3, server FTP e server SFTP) e sistemi CRM di terze parti (come [!DNL Microsoft Dynamics] e [!DNL Salesforce]).

Per ulteriori informazioni, vedere [Panoramica delle origini](../sources/home.md).

## Passaggi successivi e risorse aggiuntive

Questo documento ha fornito una breve introduzione ai diversi aspetti di [!DNL Data Ingestion] in [!DNL Experience Platform]. Continua a leggere la documentazione di panoramica di ogni metodo di assimilazione per acquisire dimestichezza con le diverse funzionalità, casi di utilizzo e procedure ottimali. Potete anche completare l’apprendimento guardando il video introduttivo che segue. Per informazioni su come [!DNL Experience Platform] tiene traccia dei metadati per i record acquisiti, consultate la [Panoramica del servizio catalogo](../catalog/home.md).

>[!WARNING]
>
>Il termine &quot;Profilo unificato&quot; utilizzato nel video seguente è obsoleto. I termini [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] sono i termini corretti utilizzati nella documentazione di [!DNL Experience Platform]. Per informazioni sulle funzionalità più recenti, consulta la documentazione.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)