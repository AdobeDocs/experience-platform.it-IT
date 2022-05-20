---
title: Note sulla versione di Adobe Experience Platform Dicembre 2019
description: Note sulla versione di dicembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 11 dicembre 2019**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal proprio [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione di Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Scheda Tipi di pubblico uniti in [!DNL Segment Builder] | La [!UICONTROL Segmenti] e [!UICONTROL Tipi di pubblico] nelle schede [!DNL Segment Builder] sono stati combinati in un unico [!UICONTROL Tipi di pubblico] scheda . Questa scheda ti consente di sfogliare e cercare i tipi di pubblico esistenti, che puoi quindi trascinare nell’area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un pubblico può aggiungere uno dei seguenti set di logica di regola alla nuova definizione del segmento: Iscrizione al pubblico come regola, set completo di logica di regola che ha definito il pubblico a cui si fa riferimento. |
| Nuova posizione per il selettore dei criteri di unione | Posizione del selettore dei criteri di unione nel [!DNL Segment Builder] è stato modificato. Per selezionare un criterio di unione per una definizione di segmento, seleziona l’icona a forma di ingranaggio **[!UICONTROL Campi]** , quindi utilizza la **[!UICONTROL Criteri di unione]** menu a discesa per selezionare il criterio di unione che si desidera utilizzare. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, consulta la sezione [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] consente di selezionare in modo programmatico e intelligente la &quot;Next Best Experience&quot; (Esperienza migliore successiva) da un set di opzioni disponibili per un determinato individuo, di distribuirle a qualsiasi canale o applicazione ed eseguire reporting e analisi.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L’ordine delle offerte per i profili ora viene derivato da una funzione di classificazione, anziché da un set fisso di offerte per tutti i profili. |

**Problemi noti**

* Nessuna.

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse fonti come soluzioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di eseguire l’autenticazione nei sistemi di storage e nei servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione streaming | L’acquisizione in streaming consente di inviare dati da dispositivi lato client e lato server a [!DNL Experience Platform] in tempo reale. La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per [!DNL Google Cloud Store] | Supporto per la raccolta dei dati da [!DNL Google Cloud Store]. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base della [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti ulteriori controlli ai campi definiti come array di oggetti per verificare che gli oggetti siano completamente definiti. Sono stati migliorati i messaggi di errore per identificare e risolvere i problemi. |

**Correzioni di bug**

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto per `eTag` per `/descriptors` punto finale [!DNL Schema Registry] API.

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull’utilizzo di XDM con [!DNL Schema Registry] API e [!DNL Schema Editor] interfaccia utente, leggere [Documentazione del sistema XDM](../../xdm/home.md).
