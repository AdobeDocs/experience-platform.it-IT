---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di Experience Platform 11 dicembre 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 dicembre 2019**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consentono di creare segmenti e generare tipi di pubblico dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Scheda Tipi di pubblico uniti in [!DNL Segment Builder] | Le schede [!UICONTROL Segments] e [!UICONTROL Audiences] in [!DNL Segment Builder] sono state combinate in un’unica scheda [!UICONTROL Audiences]. Questa scheda ti consente di sfogliare e cercare i tipi di pubblico esistenti, che puoi quindi trascinare nell’area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un pubblico può aggiungere uno dei seguenti set di logica di regola alla nuova definizione del segmento: Iscrizione al pubblico come regola, set completo di logica di regola che ha definito il pubblico a cui si fa riferimento. |
| Nuova posizione per il selettore dei criteri di unione | La posizione del selettore dei criteri di unione in [!DNL Segment Builder] è stata modificata. Per selezionare un criterio di unione per una definizione di segmento, seleziona l’icona a forma di ingranaggio nella scheda **[!UICONTROL Fields]** , quindi utilizza il menu a discesa **[!UICONTROL Merge Policy]** per selezionare il criterio di unione che desideri utilizzare. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] consente di selezionare in modo programmatico e intelligente la &quot;Migliore esperienza successiva&quot; da un set di opzioni disponibili per un singolo utente, di distribuirle a qualsiasi canale o applicazione ed eseguire reporting e analisi.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L’ordine delle offerte per i profili ora viene derivato da una funzione di classificazione, anziché da un set fisso di offerte per tutti i profili. |

**Problemi noti**

* Nessuna.

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform] . Puoi acquisire dati da diverse sorgenti, come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e il tuo sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di eseguire l’autenticazione nei sistemi di storage e nei servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione streaming | L’acquisizione in streaming ti consente di inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform] . La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per [!DNL Google Cloud Store] | Supporto per la raccolta di dati da [!DNL Google Cloud Store]. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sulle origini, consulta la [panoramica origini](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti ulteriori controlli ai campi definiti come array di oggetti per verificare che gli oggetti siano completamente definiti. Sono stati migliorati i messaggi di errore per identificare e risolvere i problemi. |

**Correzioni di bug**

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto per `eTag` per l&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry].

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39;API [!DNL Schema Registry] e l&#39;interfaccia utente [!DNL Schema Editor], consulta la [documentazione di sistema XDM](../../xdm/home.md).