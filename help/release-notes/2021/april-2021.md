---
title: Note sulla versione di Adobe Experience Platform - Aprile 2021
description: Note sulla versione di aprile 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 21 aprile 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la modifica della mappatura per i flussi di dati esistenti | Ora puoi aggiornare i set di mappatura di un flusso di dati esistente. Non puoi aggiornare i set di mappatura per i flussi di dati pianificati per un’acquisizione una tantum. Questa funzione non è supportata per API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento dei flussi di dati di origine nell’interfaccia utente](../../sources/tutorials/ui/update-dataflows.md). |
| Supporto per l’acquisizione in streaming | È ora possibile utilizzare le funzioni di preparazione dati durante la creazione di una connessione a un’origine di streaming. Per ulteriori informazioni, consulta l’esercitazione su [creazione di una connessione sorgente in streaming nell’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md). |

Per ulteriori informazioni, vedere [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) è una specifica open-source progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Raccomandazioni sugli schemi per settore | Quando selezioni classi e gruppi di campi schema nell’interfaccia utente dell’Editor schema, puoi utilizzare un nuovo filtro per visualizzare i componenti standard consigliati in base al tuo settore specifico. Consulta la documentazione su [modelli dati di settore](https://www.adobe.com/go/xdm-industry-erds-en) per ulteriori informazioni su come questi componenti si relazionano tra loro per diversi casi d’uso del settore. |

## [!DNL Intelligent Services] {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science.

### IA per l’analisi dei clienti

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati di Adobe Analytics tramite il connettore di origine di Analytics senza la necessità di effettuare l’ETL dei dati per adeguarli allo schema Consumer Experience Event (CEE). |
| Supporto per i dati di Adobe Audience Manager | È stata aggiornata la funzionalità per supportare i set di dati di Adobe Audience Manager tramite il connettore di origine di Audience Manager senza la necessità di effettuare l’ETL dei dati per adeguarli allo schema Consumer Experience Event (CEE). |
| Riepilogo prestazioni modello | Customer AI ora dispone di un [scheda riepilogo prestazioni modello](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) nella pagina approfondimenti dell’istanza del servizio. La scheda Prestazioni modello mostra tutte le velocità di conversione e di abbandono effettive. Questo ti consente di decifrare e capire cosa accade in ciascun bucket di propensione. |

Per ulteriori informazioni sui set di dati supportati, consulta [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati di Adobe Analytics tramite il connettore di origine di Analytics senza la necessità di effettuare l’ETL dei dati per adeguarli allo schema Consumer Experience Event (CEE). |

Per ulteriori informazioni sui set di dati supportati, consulta [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal tuo [!DNL Real-Time Customer Profile] dati. Questi segmenti sono configurati e gestiti centralmente su Platform, rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni di aggregazione aggiuntive | Sono state aggiunte funzioni di conteggio nel Generatore di segmenti. Le funzioni di conteggio consentono di contare il numero di volte in cui l’evento specificato è stato eseguito. Ulteriori informazioni sulle funzioni di conteggio sono disponibili nella sezione delle funzioni di conteggio del [Guida al Generatore di segmenti](../../segmentation/ui/segment-builder.md#count-functions) |

Per ulteriori informazioni su [!DNL Segmentation Service], consultare il [Panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ora puoi creare una [!DNL Marketo Engage] connessione di origine tramite l’interfaccia utente di per portare i dati B2B in Platform e tenerli aggiornati utilizzando le applicazioni connesse a Platform. Per ulteriori informazioni, vedere [[!DNL Marketo Engage] documentazione del connettore di origine](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Sorgenti beta che passano a GA | Le seguenti sorgenti sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
