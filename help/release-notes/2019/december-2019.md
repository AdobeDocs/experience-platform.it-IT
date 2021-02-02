---
title: Note sulla versione di Adobe Experience Platform
description: ' Experience Platform note sulla versione 11 dicembre 2019'
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '650'
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

Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai dati [!DNL Real-time Customer Profile]. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione  Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Scheda Pubblico unito in [!DNL Segment Builder] | Le schede [!UICONTROL Segments] e [!UICONTROL Audiences] nella [!DNL Segment Builder] sono state combinate in una singola scheda [!UICONTROL Audiences]. Questa scheda consente di individuare e cercare audience esistenti, che potete quindi trascinare e rilasciare nell&#39;area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un&#39;audience può aggiungere uno dei seguenti set di regole logiche alla nuova definizione di segmento: Iscrizione dell&#39;audience come regola, L&#39;intero set di logica di regole che ha definito l&#39;audience di riferimento. |
| Nuova posizione per il selettore dei criteri di unione | La posizione del selettore dei criteri di unione in [!DNL Segment Builder] è stata modificata. Per selezionare un criterio di unione per la definizione di un segmento, selezionate l&#39;icona a forma di ingranaggio nella scheda **[!UICONTROL Fields]**, quindi utilizzate il menu a discesa **[!UICONTROL Merge Policy]** per selezionare il criterio di unione che desiderate utilizzare. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, vedere la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] consente di selezionare in modo programmatico e intelligente &quot;Next Best Experience&quot; da una serie di opzioni disponibili per un determinato individuo, di distribuirle a qualsiasi canale o applicazione, nonché di eseguire reporting e analisi.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L&#39;ordine delle offerte per i profili ora viene derivato tramite una funzione di classificazione, anziché tramite un set fisso di offerte per tutti i profili. |

**Problemi noti**

* Nessuna.

## [!DNL Sources] {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. È possibile acquisire dati da origini diverse, come  soluzioni di Adobe, storage basato su cloud, software di terze parti e il sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di effettuare l&#39;autenticazione ai sistemi di storage e ai servizi CRM, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione di streaming | L&#39;assimilazione dello streaming consente di inviare in tempo reale dati da dispositivi lato client e lato server a [!DNL Experience Platform]. La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per [!DNL Google Cloud Store] | Supporto per la raccolta di dati da [!DNL Google Cloud Store]. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sulle origini, vedere la [panoramica delle origini](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM)  {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi di Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti controlli aggiuntivi ai campi definiti come array di oggetti per assicurare che gli oggetti siano completamente definiti. Messaggi di errore migliorati per identificare e risolvere i problemi. |

**Correzioni di bug**

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto per `eTag` per l&#39;endpoint `/descriptors` nell&#39;API [!DNL Schema Registry].

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39;interfaccia utente [!DNL Schema Registry] API e [!DNL Schema Editor], consultare la [Documentazione di sistema XDM](../../xdm/home.md).