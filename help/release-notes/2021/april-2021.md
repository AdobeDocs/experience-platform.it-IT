---
title: Note sulla versione di Adobe Experience Platform - Aprile 2021
description: Le note sulla versione di aprile 2021 per Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 10%

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
| Supporto per la modifica della mappatura per i flussi di dati esistenti | Ora puoi aggiornare i set di mappatura di un flusso di dati esistente. Non è possibile aggiornare i set di mappatura per i flussi di dati pianificati per un’acquisizione una tantum. Questa funzione non è supportata per le API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Per ulteriori informazioni, consulta l’esercitazione su [aggiornamento dei flussi di dati di origini nell’interfaccia utente](../../sources/tutorials/ui/update-dataflows.md). |
| Supporto per l’acquisizione in streaming | È ora possibile utilizzare le funzioni di preparazione dei dati durante la creazione di una connessione sorgente di streaming. Per ulteriori informazioni, consulta l’esercitazione su [creazione di una connessione sorgente in streaming nell’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md). |

Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) è una specifica open-source progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Raccomandazioni in base allo schema per settore | Quando si selezionano le classi e i gruppi di campi dello schema nell’interfaccia utente dell’Editor di schema, è possibile utilizzare un nuovo filtro per visualizzare i componenti standard consigliati in base al settore specifico. Consulta la documentazione su [modelli di dati del settore](https://www.adobe.com/go/xdm-industry-erds-en) per ulteriori informazioni su come questi componenti si relazionano tra loro per diversi casi d’uso nel settore. |

## [!DNL Intelligent Services] {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello di business senza la necessità di competenze scientifiche in materia di dati.

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati Adobe Analytics tramite il connettore di origine Analytics senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |
| Supporto per i dati Adobe Audience Manager | È stata aggiornata la funzionalità per supportare i set di dati Adobe Audience Manager tramite il connettore di origine Audience Manager senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |
| Riepilogo delle prestazioni del modello | L’intelligenza artificiale del cliente ora ha un [scheda riepilogo prestazioni modello](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) nella pagina approfondimenti dell’istanza del servizio. La scheda Prestazioni del modello mostra tutti i tassi di conversione e di abbandono effettivi. Questo ti permette di decifrare e capire cosa succede in ogni tuo blocco di propensione. |

Per ulteriori informazioni sui set di dati supportati, consulta la sezione [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati Adobe Analytics tramite il connettore di origine Analytics senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |

Per ulteriori informazioni sui set di dati supportati, consulta la sezione [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal proprio [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su Platform, rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni di aggregazione aggiuntive | Le funzioni di conteggio sono state aggiunte nel Generatore di segmenti. Le funzioni di conteggio consentono di contare il numero di volte in cui l’evento specificato è stato eseguito. Ulteriori informazioni sulle funzioni di conteggio sono disponibili nella sezione delle funzioni di conteggio del [Guida al Generatore di segmenti](../../segmentation/ui/segment-builder.md#count-functions) |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ora puoi creare una [!DNL Marketo Engage] connessione di origine tramite l’interfaccia utente per portare i dati B2B in Platform e tenerli aggiornati utilizzando le applicazioni connesse a Platform. Per ulteriori informazioni, consulta la sezione [[!DNL Marketo Engage] documentazione del connettore di origine](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Sorgenti beta che si spostano in GA | Le seguenti origini sono state promosse dalla versione beta a GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
