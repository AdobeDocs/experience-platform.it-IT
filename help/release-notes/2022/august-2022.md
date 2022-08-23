---
title: Note sulla versione di Adobe Experience Platform - Agosto 2022
description: Note sulla versione di agosto 2022 per Adobe Experience Platform.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 24 agosto 2022**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Preparazione dei dati](#data-prep)
- [Origini](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per l’acquisizione di record con avvisi | In Preparazione dati gli avvisi (errori non critici) verranno localizzati nei campi e il resto della riga potrà essere acquisito. Tutti gli errori di trasformazione della mappatura vengono ora segnalati come avvisi e le righe parzialmente ingerite vengono considerate di successo, con un avviso.  Il monitoraggio è supportato anche nei record con avvisi e dettagli diagnostici. L’acquisizione parziale di record con avvisi è attualmente disponibile solo per i dati in streaming. Consulta la documentazione su [acquisizione di record con avvisi](../../sources/tutorials/ui/monitor-streaming.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto tra aree geografiche per l’origine Adobe Analytics | È ora possibile acquisire suite di rapporti da qualsiasi regione (Stati Uniti, Regno Unito o Singapore). Le suite di rapporti devono essere mappate nella stessa organizzazione dell’istanza Sandbox di Experience Platform in cui viene creata la connessione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Adobe Analytics nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
