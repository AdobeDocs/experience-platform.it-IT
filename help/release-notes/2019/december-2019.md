---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' Experience Platform note sulla versione 11 dicembre 2019'
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 dicembre 2019**

Aggiornamenti alle funzionalità esistenti in  Adobe Experience Platform:

* [!DNL Segmentation Service](#segmentation)
* [!DNL Decisioning Service](#decisioning)
* [!DNL Sources](#sources)
* [!DNL Experience Data Model (XDM) System](#xdm)

## [!DNL Segmentation Service] {#segmentation}

 Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione  Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Scheda Pubblico unito in [!DNL Segment Builder] | Le schede [!UICONTROL _Segmenti _]e[!UICONTROL _Pubblico_] di [!DNL Segment Builder] sono state combinate in una singola scheda [!UICONTROL _Audience _]. Questa scheda consente di individuare e cercare audience esistenti, che potete quindi trascinare e rilasciare nell&#39;area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un&#39;audience può aggiungere uno dei seguenti set di regole logiche alla nuova definizione di segmento: Iscrizione dell&#39;audience come regola, L&#39;intero set di logica di regole che ha definito l&#39;audience di riferimento. |
| Nuova posizione per il selettore dei criteri di unione | La posizione del selettore dei criteri di unione nell&#39; [!DNL Segment Builder] area è stata modificata. Per selezionare un criterio di unione per una definizione di segmento, fai clic sull&#39;icona a forma di ingranaggio nella scheda [!UICONTROL _Campi _], quindi utilizza il menu a_[!UICONTROL Merge Policy]_ discesa per selezionare il criterio di unione che desideri utilizzare. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, consulta la panoramica [del servizio di](../../segmentation/home.md)segmentazione.

## [!DNL Decisioning Service] {#decisioning}

 Adobe Experience Platform [!DNL Decisioning Service] consente di selezionare in modo programmatico e intelligente &quot;Next Best Experience&quot; da una serie di opzioni disponibili per un determinato individuo, di distribuirle a qualsiasi canale o applicazione, nonché di eseguire reporting e analisi.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L&#39;ordine delle offerte per i profili ora viene derivato tramite una funzione di classificazione, anziché tramite un set fisso di offerte per tutti i profili. |

**Problemi noti**

* Nessuna.

Per un&#39;introduzione completa al servizio, consultate la panoramica [del servizio](../../decisioning-service/home.md) Decisioning.

## [!DNL Sources] {#sources}

 Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare i dati utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come  soluzioni di Adobe, storage basato su cloud, software di terze parti e il sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di effettuare l&#39;autenticazione ai sistemi di storage e ai servizi CRM, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione di streaming | L’assimilazione dello streaming consente di inviare dati da dispositivi lato client e lato server [!DNL Experience Platform] in tempo reale. La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per [!DNL Google Cloud Store] | Supporto per la raccolta di dati da [!DNL Google Cloud Store]. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi  Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti controlli aggiuntivi ai campi definiti come array di oggetti per assicurare che gli oggetti siano completamente definiti. Messaggi di errore migliorati per identificare e risolvere i problemi. |

**Correzioni di bug**

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto `eTag` per l&#39; `/descriptors` endpoint nell&#39; [!DNL Schema Registry] API.

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM tramite l&#39; [!DNL Schema Registry] API e l&#39;interfaccia [!DNL Schema Editor] utente, consulta la documentazione [di sistema](../../xdm/home.md)XDM.