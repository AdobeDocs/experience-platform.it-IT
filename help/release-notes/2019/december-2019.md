---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 11 dicembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Note sulla versione di Adobe Experience Platform

## Data di rilascio: 11 dicembre 2019

## Servizio di segmentazione

Il servizio di segmentazione di Adobe Experience Platform fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai dati del profilo cliente in tempo reale. Questi segmenti sono configurati e mantenuti a livello centrale sulla piattaforma, rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

Il servizio di segmentazione definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Scheda Pubblico unito in Segment Builder (Generatore di segmenti) | Le schede _Segmenti_ e _Pubblico_ nel Generatore di segmenti sono state combinate in una singola scheda _Audience_ . Questa scheda consente di individuare e cercare audience esistenti, che potete quindi trascinare e rilasciare nell&#39;area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un&#39;audience può aggiungere uno dei seguenti set di regole logiche alla nuova definizione di segmento: Iscrizione dell&#39;audience come regola, L&#39;intero set di logica di regole che ha definito l&#39;audience di riferimento. |
| Nuova posizione per il selettore dei criteri di unione | La posizione del selettore dei criteri di unione nel Generatore di segmenti è stata modificata. Per selezionare un criterio di unione per una definizione di segmento, fai clic sull&#39;icona a forma di ingranaggio nella scheda _Campi_ , quindi utilizza il menu a discesa _Unisci criterio_ per selezionare il criterio di unione che desideri utilizzare. |

### Problemi noti

* None

Per ulteriori informazioni, consulta la panoramica [del servizio di](../../segmentation/home.md)segmentazione.

## Servizio di disattivazione

Adobe Experience Platform Decisioning Service consente di selezionare in modo programmatico e intelligente la &quot;Next Best Experience&quot; tra una serie di opzioni disponibili per un determinato individuo, distribuirla a qualsiasi canale o applicazione ed eseguire reporting e analisi.

### Nuove funzionalità

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L&#39;ordine delle offerte per i profili ora viene derivato tramite una funzione di classificazione, anziché tramite un set fisso di offerte per tutti i profili. |

### Problemi noti

* None.

Per un&#39;introduzione completa al servizio, consultate la panoramica [del servizio](../../decisioning-service/home.md) Decisioning.

## Origini

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di effettuare l&#39;autenticazione ai sistemi di storage e ai servizi CRM, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

### Nuove funzionalità

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione di streaming | L’assimilazione dello streaming consente di inviare in tempo reale dati da dispositivi lato client e lato server a Experience Platform. La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per Google Cloud Store | Supporto per la raccolta di dati da Google Cloud Store. |

### Problemi noti

* None.

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).

## Sistema XDM (Experience Data Model)

Standardizzazione e interoperabilità sono concetti chiave della piattaforma Experience. Experience Data Model (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che desideri comunicare con i servizi in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

### Nuove funzionalità

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti controlli aggiuntivi ai campi definiti come array di oggetti per assicurare che gli oggetti siano completamente definiti. Messaggi di errore migliorati per identificare e risolvere i problemi. |

### Correzioni di bug

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto `eTag` per l&#39; `/descriptors` endpoint nell&#39;API del Registro di sistema dello schema.

### Problemi noti

* None

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39;interfaccia utente API del Registro di sistema e Editor schema, consultare la documentazione [di sistema](../../xdm/home.md)XDM.