---
title: Note sulla versione di Adobe Experience Platform - Aprile 2020
description: Note sulla versione di Adobe Experience Platform di aprile 2020.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: note sulla versione;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 15%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 8 aprile 2020**

Nuove funzioni di Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governance dei dati](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] consente agli analisti e ai professionisti del marketing di sfruttare la potenza dell&#39;intelligenza artificiale e dell&#39;apprendimento automatico nei casi di utilizzo dell&#39;esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science. Inoltre, i professionisti del marketing possono attivare le previsioni in applicazioni Adobe Experience Cloud, Adobe Experience Platform e di terze parti.

**Funzioni principali**

| Funzione | Descrizione |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] offre agli esperti di marketing la possibilità di generare previsioni sui clienti a livello individuale con le relative spiegazioni. Grazie a fattori influenti, [!DNL Customer AI] può dirti cosa potrebbe fare un cliente e perché. Inoltre, gli esperti di marketing possono trarre vantaggio dalle previsioni e dalle informazioni di [!DNL Customer AI] per personalizzare le esperienze dei clienti fornendo le offerte e i messaggi più appropriati. |
| [!DNL Attribution AI] | [!DNL Attribution AI] è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a risultati specifici. Con [!DNL Attribution AI], gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l&#39;impatto di ogni singola interazione con i clienti in ogni fase dei percorsi dei clienti. |

**Problemi noti**

* Nessun problema noto.

Per ulteriori informazioni su [!DNL Intelligent Services] e sulle sue caratteristiche, consulta la [Panoramica di Intelligent Services](../../intelligent-services/home.md).

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull&#39;esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Informazioni visualizzazione alternativa automatica | [!DNL Schema Registry] applica automaticamente i valori personalizzati del titolo e della descrizione configurati nel descrittore `alternateDisplayInfo`. |
| Limitazioni dei campi scalari | [!DNL Schema Registry] non consente più di 6000 campi scalari in un singolo schema. |
| Revisione delle prestazioni | [!DNL Schema Registry] è stato revisionato per eseguire e soddisfare le richieste di [!DNL Experience Platform] in modo migliore. |

**Correzioni di bug**

* XDM è stato aggiornato a XED convertito per supportare un formato XED più pulito per i campi URI nidificati in XDM standard.

**Problemi noti**

* Noto

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati della clientela e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dati, etichettatura di utilizzo dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

La guida introduttiva alla governance dei dati richiede una comprensione approfondita delle normative, degli obblighi contrattuali e delle politiche aziendali applicabili ai dati dei clienti. Da lì, i dati possono essere classificati applicando le etichette di utilizzo dei dati appropriate e il loro utilizzo può essere controllato tramite la definizione di criteri di utilizzo dei dati.

Il framework di governance dei dati semplifica e semplifica il processo di categorizzazione dei dati e di creazione di criteri di utilizzo dei dati tramite l&#39;interfaccia utente [!DNL Experience Platform] e l&#39;API [!DNL Policy Service].

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Gestire i criteri di utilizzo dei dati nell’interfaccia utente | È ora possibile gestire i criteri di utilizzo dei dati nell&#39;area di lavoro **Criteri** nell&#39;interfaccia utente [!DNL Experience Platform]. Per ulteriori informazioni, vedere la [guida utente](../../data-governance/policies/user-guide.md) dei criteri. |

**Problemi noti**

* Nessuno.

Per ulteriori informazioni, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).


## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Real-Time CDP ora supporta l&#39;attivazione dei dati per oltre cinquanta estensioni [!DNL Experience Cloud Launch], abilitando analisi, personalizzazione e altri casi d&#39;uso. Per ulteriori informazioni, consulta:

| Documentazione | Descrizione |
|--- | ---|
| [Tipi e categorie di destinazione](../../destinations/destination-types.md) | Questo articolo spiega la differenza tra connessioni ed estensioni nell&#39;interfaccia di Real-Time CDP e consiglia quando utilizzare ciascuna di queste destinazioni. |
| [Estensioni di Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Questa pagina spiega cosa sono le estensioni [!DNL Launch], elenca i casi di utilizzo e i collegamenti alla documentazione per ciascuna estensione [!DNL Launch] in Real-Time CDP. |

Per ulteriori informazioni, consulta la [Panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Nuove norme legali e organizzative danno agli utenti il diritto di accedere ai propri dati personali o di cancellarli dagli archivi di dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire queste richieste di dati dei clienti. Con [!DNL Privacy Service] è possibile inviare richieste di accesso ed eliminazione di dati personali o privati dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di accesso ai dati personali possono ora essere create e monitorate in base alla legge sulla protezione dei dati personali (PDPA) in Thailandia. Quando si eseguono richieste di accesso a dati personali nell&#39;API, l&#39;array `regulation` accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di spazio dei nomi nell’interfaccia utente | È ora possibile specificare diversi tipi di spazio dei nomi nel Generatore di richieste nell&#39;interfaccia utente [!DNL Privacy Service]. Per ulteriori informazioni, consulta la [guida utente](../../privacy-service/ui/user-guide.md). |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

Problemi noti

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service], leggere la [panoramica Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo consentire di strutturare, etichettare e migliorare tali dati utilizzando i servizi [!DNL Platform]. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di configurare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto API e interfaccia utente per i database | Nuovi connettori di origine per [!DNL Apache Spark] (su HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (su HDInsights) e [!DNL Phoenix]. |
| Supporto API e interfaccia utente per applicazioni basate su pagamenti | Nuovi connettori di origine per [!DNL PayPal]. |
| Supporto di API e interfaccia utente per applicazioni basate su protocolli | Nuovi connettori di origine per [!DNL Generic OData]. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
