---
title: Note sulla versione di Adobe Experience Platform dicembre 2019
description: Note sulla versione di dicembre 2019 per Adobe Experience Platform.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
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

Il servizio di segmentazione di Adobe Experience Platform fornisce un’interfaccia utente e un’API RESTful che consente di creare segmenti e generare tipi di pubblico dal tuo [!DNL Real-Time Customer Profile] dati. Questi segmenti sono configurati e gestiti centralmente su [!DNL Platform], rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Scheda Tipi di pubblico uniti in [!DNL Segment Builder] | Il [!UICONTROL Segmenti] e [!UICONTROL Tipi di pubblico] schede in [!DNL Segment Builder] sono stati combinati in un unico [!UICONTROL Tipi di pubblico] scheda. Questa scheda ti consente di sfogliare e cercare i tipi di pubblico esistenti, che puoi quindi trascinare nell’area di lavoro del generatore di regole per creare una nuova definizione di segmento. Il riferimento a un pubblico può aggiungere uno dei seguenti set di logica della regola alla nuova definizione del segmento: Appartenenza al pubblico come regola, L’intero set di logica della regola che ha definito il pubblico di riferimento. |
| Nuova posizione per il selettore dei criteri di unione | Posizione del selettore dei criteri di unione nel [!DNL Segment Builder] è stato modificato. Per selezionare un criterio di unione per la definizione di un segmento, seleziona l’icona a forma di ingranaggio nella **[!UICONTROL Campi]** , quindi utilizza **[!UICONTROL Criterio di unione]** menu a discesa per selezionare il criterio di unione da utilizzare. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni, vedere [Panoramica del servizio di segmentazione](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] consente di selezionare in modo programmatico e intelligente la &quot;Migliore esperienza successiva&quot; da una serie di opzioni disponibili per un determinato individuo, distribuirla a qualsiasi canale o applicazione ed eseguire attività di reporting e analisi.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Funzioni di classificazione | L’ordine delle offerte per i profili ora viene derivato tramite una funzione di classificazione, anziché da un set fisso di offerte per tutti i profili. |

**Problemi noti**

* Nessuna.

## [!DNL Sources] {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio soluzioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di configurare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di eseguire l’autenticazione nei sistemi di storage e nei servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ---------- | ------------ |
| Connessione streaming | L’acquisizione in streaming ti consente di inviare dati da dispositivi lato client e lato server a [!DNL Experience Platform] in tempo reale. La versione include una nuova interfaccia utente per la connessione in streaming. |
| Supporto del connettore per [!DNL Google Cloud Store] | Supporto per la raccolta di dati da [!DNL Google Cloud Store]. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni sulle origini, vedere [panoramica sulle origini](../../sources/home.md).

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
|--- | ---|
| Convalida dello schema migliorata | Nuovi controlli per garantire che i riferimenti vengano risolti in campi aggiuntivi come previsto. Sono stati aggiunti controlli aggiuntivi ai campi definiti come array di oggetti per verificare che gli oggetti siano completamente definiti. Sono stati migliorati i messaggi di errore per identificare e risolvere i problemi. |

**Correzioni di bug**

* Manutenzione e miglioramenti relativi al controllo degli accessi e alle sandbox.
* Supporto per `eTag` per `/descriptors` endpoint nella [!DNL Schema Registry] API.

**Problemi noti**

* Nessuna

Per ulteriori informazioni sull&#39;utilizzo di XDM con [!DNL Schema Registry] API e [!DNL Schema Editor] dell&#39;interfaccia utente, leggere il [Documentazione del sistema XDM](../../xdm/home.md).
