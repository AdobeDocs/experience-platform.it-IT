---
title: Note sulla versione di Adobe Experience Platform
description: ' note sulla versione del Experience Platform 27 gennaio 2021'
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: cf70b21f3a8c02b25e5acd3be8c8feaa3f52a5e3
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 8%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 27 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente agli sviluppatori di dati di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni di espressione regolari | [!DNL Data Prep] Mapper ora supporta la corrispondenza e l&#39;estrazione di parte del campo di input in base alle espressioni regolari. |

Per ulteriori informazioni, vedere la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati tramite i servizi Piattaforma. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

 Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Miglioramenti al connettore sorgente Adobe Audience Manager | Ora puoi filtrare e selezionare singoli segmenti di prime parti da  Audience Manager a caricamento in piattaforma, nonché filtrare le caratteristiche di prime parti. Per ulteriori informazioni, vedere l&#39;esercitazione su [creazione di un connettore di origine del Audience Manager ](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] miglioramenti al connettore di origine | È ora possibile acquisire file di dimensioni superiori a 10 GB in un&#39;esecuzione di flusso utilizzando il connettore sorgente [!DNL BigQuery]. Per ulteriori informazioni, vedere [[!DNL BigQuery] panoramica del connettore di origine](../../sources/connectors/databases/bigquery.md). |
| Supporto per tipi di dati complessi per gli storage cloud | Ora è possibile assimilare tipi di dati complessi, come array in file JSON, quando si utilizza un connettore origine di archiviazione cloud. Per ulteriori informazioni, vedere le esercitazioni sulla creazione di un flusso di dati di archiviazione cloud [nell&#39;interfaccia utente](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) o [tramite l&#39;API [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md). |
| Supporto per l&#39;autenticazione basata sulle chiavi dell&#39;entità del servizio per l&#39;origine [!DNL Microsoft Dynamics] | Ora puoi eseguire l&#39;autenticazione sul tuo account [!DNL Dynamics] utilizzando una chiave dell&#39;entità del servizio come alternativa all&#39;autenticazione basata su password. Per ulteriori informazioni, vedere [[!DNL Dynamics] panoramica del connettore di origine](../../sources/connectors/crm/ms-dynamics.md). |

Per ulteriori informazioni sulle origini, vedere la [panoramica delle origini](../../sources/home.md).
