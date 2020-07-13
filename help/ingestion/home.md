---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sull'inserimento dei dati  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---


# Panoramica sull&#39;inserimento dei dati

 Adobe Experience Platform riunisce i dati provenienti da più origini per aiutare gli addetti al marketing a comprendere meglio il comportamento dei loro clienti.  Adobe Experience Platform Data Ingestion rappresenta i diversi metodi mediante i quali [!DNL Platform] vengono acquisiti i dati da tali origini, nonché il modo in cui tali dati vengono memorizzati all&#39;interno del Data Lake per essere utilizzati dai [!DNL Platform] servizi a valle.

Questo documento presenta i tre modi principali in cui i dati vengono trasferiti [!DNL Platform], con collegamenti alla rispettiva documentazione di panoramica per informazioni più dettagliate.

## Caricamento batch

L’assimilazione batch consente di assimilare i dati in [!DNL Experience Platform] file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Una volta acquisiti, i batch forniscono i metadati che descrivono il numero di record correttamente acquisiti, nonché tutti i record con errore e i messaggi di errore associati.

I file di dati caricati manualmente, come file CSV semplici (mappati a schemi XDM) e i fotogrammi di dati Parquet, devono essere acquisiti con questo metodo.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione dei](./batch-ingestion/overview.md) batch.

## Caricamento in streaming

L’assimilazione dello streaming consente di inviare dati da dispositivi lato client e lato server [!DNL Experience Platform] in tempo reale. [!DNL Platform] supporta l&#39;utilizzo di insenature di dati per lo streaming di dati esperienza in arrivo, persistenti nei set di dati abilitati per lo streaming all&#39;interno del Data Lake. È possibile configurare le ingressi dei dati per l&#39;autenticazione automatica dei dati raccolti, garantendo che i dati provengano da un&#39;origine affidabile.

Per ulteriori informazioni, consulta la panoramica [sull’assimilazione](./streaming-ingestion/overview.md) in streaming.

## Origini

[!DNL Experience Platform] consente di impostare connessioni di origine a vari provider di dati. Queste connessioni consentono di eseguire l&#39;autenticazione alle origini dati esterne, impostare i tempi di esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione.

Le connessioni di origine possono essere configurate per raccogliere dati da altre applicazioni Adobe (come Adobe  Analytics e  Adobe Audience Manager), origini di archiviazione cloud di terze parti (come [!DNL Azure Blob], [!DNL Amazon] S3, server FTP e server SFTP) e sistemi CRM di terze parti (come Microsoft Dynamics e Salesforce).

Per ulteriori informazioni, consulta la panoramica [](../sources/home.md) Origini.

## Passaggi successivi e risorse aggiuntive

Questo documento ha fornito una breve introduzione ai diversi aspetti di [!DNL Data Ingestion] in [!DNL Experience Platform]. Continua a leggere la documentazione di panoramica di ogni metodo di assimilazione per acquisire dimestichezza con le diverse funzionalità, casi di utilizzo e procedure ottimali. Potete anche completare l’apprendimento guardando il video della panoramica sull’assimilazione riportato di seguito. Per informazioni su come [!DNL Experience Platform] tenere traccia dei metadati per i record acquisiti, consultate la panoramica [del servizio](../catalog/home.md)catalogo.

>[!WARNING]
>
> Il termine &quot;Profilo unificato&quot; utilizzato nel video seguente è obsoleto. I termini [!DNL "Profile"] o [!DNL "Real-time Customer Profile"] i termini corretti utilizzati nella [!DNL Experience Platform] documentazione. Per informazioni sulle funzionalità più recenti, consulta la documentazione.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)