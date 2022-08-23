---
title: Note sulla versione di Adobe Experience Platform - Agosto 2022
description: Note sulla versione di agosto 2022 per Adobe Experience Platform.
source-git-commit: b8513fa214ea74eec6809796cc194466e05cbb21
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 6%

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
| Disponibilità generale delle origini self-service (SDK batch) | Sviluppa, testa e integra la tua origine dati basata su API REST per acquisire dati batch in Experience Platform utilizzando specifiche sorgente facili da configurare. Con l&#39;SDK di Origini puoi: <ul><li>Configura una nuova origine per il catalogo di Experience Platform.</li><li>Definisci le specifiche dell’origine, incluse le informazioni relative ai tipi di autenticazione supportati, alla pianificazione e al modo in cui vengono recuperati i dati delle risorse.</li><li>Crea la documentazione rivolta all’utente per la nuova sorgente.</li></ul> Per ulteriori informazioni, consulta la documentazione su [Sorgenti self-service (SDK batch)](../../sources/sources-sdk/overview.md). |
| Disponibilità generale [!DNL Google BigQuery] source | Utilizza la [!DNL Google BigQuery] sorgente per acquisire i dati dal [!DNL Google BigQuery] data warehouse ad Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] sorgente (Beta) | Utilizza la [!DNL Teradata Vantage] da origine a acquisizione di dati da ambienti multi-cloud ibridi ad Experience Platform. Per ulteriori informazioni, consulta la documentazione sul [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Supporto tra aree geografiche per l’origine Adobe Analytics | È ora possibile acquisire suite di rapporti da qualsiasi regione (Stati Uniti, Regno Unito o Singapore). Le suite di rapporti devono essere mappate nella stessa organizzazione dell’istanza Sandbox di Experience Platform in cui viene creata la connessione sorgente. Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Adobe Analytics nell’interfaccia utente](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| Supporto API per l’acquisizione on-demand | Utilizza l’acquisizione on-demand per creare esecuzioni di flussi ad hoc per un determinato flusso di dati con [!DNL Flow Service] API. Le esecuzioni di flusso create devono essere impostate su acquisizione una tantum. Per ulteriori informazioni, consulta la guida su [creazione di un’esecuzione di flusso per l’acquisizione on-demand tramite API](../../sources/tutorials/api/on-demand-ingestion.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
