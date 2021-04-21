---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform per il 21 aprile 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 875d3838e16a3b79fa9ab3ec61e4ffb15ea1cf20
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 12%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 21 aprile 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per la modifica della mappatura per i flussi di dati esistenti | Ora puoi aggiornare i set di mappatura di un flusso di dati esistente. Non è possibile aggiornare i set di mappatura per i flussi di dati pianificati per un’acquisizione una tantum. Questa funzione non è supportata per le API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Per ulteriori informazioni, consulta l’esercitazione sull’ [aggiornamento dei flussi di dati di origini nell’interfaccia utente](../../sources/tutorials/ui/update-dataflows.md). |
| Supporto per l’acquisizione in streaming | È ora possibile utilizzare le funzioni di preparazione dei dati durante la creazione di una connessione sorgente di streaming. Per ulteriori informazioni, consulta l’esercitazione su [creazione di una connessione sorgente di streaming nell’interfaccia utente](../../sources/tutorials/ui/create/streaming/http.md). |

Per ulteriori informazioni, consulta la [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello di business senza la necessità di competenze scientifiche in materia di dati.

### Customer AI

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati Adobe Analytics tramite il connettore di origine Analytics senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |
| Supporto per i dati Adobe Audience Manager | È stata aggiornata la funzionalità per supportare i set di dati Adobe Audience Manager tramite il connettore di origine Audience Manager senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |
| Riepilogo delle prestazioni del modello | Customer AI dispone ora di una [scheda di riepilogo delle prestazioni del modello](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) nella pagina delle informazioni sull&#39;istanza del servizio. La scheda Prestazioni del modello mostra tutti i tassi di conversione e di abbandono effettivi. Questo ti permette di decifrare e capire cosa succede in ogni tuo blocco di propensione. |

Per ulteriori informazioni sui set di dati supportati, consulta la [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto per i dati di Adobe Analytics | È stata aggiornata la funzionalità per supportare i set di dati Adobe Analytics tramite il connettore di origine Analytics senza la necessità di ETL dei dati per conformarsi allo schema CEE (Consumer Experience Event). |

Per ulteriori informazioni sui set di dati supportati, consulta la [[!DNL Intelligent Services] documentazione sulla preparazione dei dati](../../intelligent-services/data-preparation.md).

## Servizio di segmentazione {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzioni di aggregazione aggiuntive | Le funzioni di conteggio sono state aggiunte nel Generatore di segmenti. Le funzioni di conteggio consentono di contare il numero di volte in cui l’evento specificato è stato eseguito. Ulteriori informazioni sulle funzioni di conteggio sono disponibili nella sezione delle funzioni di conteggio della [guida del Generatore di segmenti](../../segmentation/ui/segment-builder.md#count-functions) |

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).


## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Ora puoi creare una connessione sorgente [!DNL Marketo Engage] utilizzando l’interfaccia utente per inserire i dati B2B in Platform e aggiornarli utilizzando le applicazioni connesse a Platform. Per ulteriori informazioni, consulta la [[!DNL Marketo Engage] documentazione del connettore di origine](../../sources/connectors/adobe-applications/marketo/marketo.md). |

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).
