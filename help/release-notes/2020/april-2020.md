---
title: Note sulla versione di Adobe Experience Platform - Aprile 2020
description: Le note sulla versione di aprile 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: note sulla versione;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: e08deb8bea7f02639b680c4988522627de82bdee
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 8 aprile 2020**

Nuove funzioni in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governance dei dati](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] consente agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso della customer experience. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un&#39;azienda utilizzando configurazioni a livello di business senza la necessità di conoscenze scientifiche dei dati. Inoltre, i professionisti del marketing possono attivare le previsioni in applicazioni Adobe Experience Cloud, Adobe Experience Platform e di terze parti.

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] fornisce agli esperti di marketing il potere di generare previsioni dei clienti a livello individuale con spiegazioni. Con l&#39;aiuto di fattori influenti, [!DNL Customer AI] può spiegarti cosa è probabile che faccia un cliente e perché. Inoltre, gli esperti di marketing possono trarre vantaggio da [!DNL Customer AI] previsioni e insights per personalizzare le esperienze dei clienti servendo le offerte e i messaggi più appropriati. |
| [!DNL Attribution AI] | [!DNL Attribution AI] è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici. Con [!DNL Attribution AI], gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l’impatto di ogni singola interazione con i clienti in ogni fase del percorso del cliente. |

**Problemi noti**

* Nessun problema noto al momento.

Per ulteriori informazioni su [!DNL Intelligent Services] e ciò che ha da offrire, vedi [Panoramica di Intelligent Services](../../intelligent-services/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base della [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da un Adobe, è uno sforzo per standardizzare i dati sulla customer experience e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare il potere delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che offre informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Informazioni di visualizzazione alternative automatiche | La [!DNL Schema Registry] applica automaticamente i valori personalizzati del titolo e della descrizione configurati nel `alternateDisplayInfo` descrittore. |
| Restrizioni dei campi scalari | La [!DNL Schema Registry] non consente più di 6000 campi scalari in un singolo schema. |
| Revisione delle prestazioni | La [!DNL Schema Registry] è stato modificato per soddisfare le richieste di [!DNL Experience Platform] meglio. |

**Correzioni di bug**

* È stato aggiornato XDM in XED convertito per supportare un formato XED più pulito per i campi URI nidificati in XDM standard.

**Problemi noti**

* Conosciuto

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo dell’accesso ai dati per le azioni di marketing.

Per iniziare a utilizzare la governance dei dati è necessaria una comprensione approfondita delle normative, degli obblighi contrattuali e delle politiche aziendali applicabili ai dati dei clienti. Da lì, i dati possono essere classificati applicando le etichette di utilizzo dei dati appropriate e il loro utilizzo può essere controllato tramite la definizione di criteri di utilizzo dei dati.

Il framework per la governance dei dati semplifica e semplifica il processo di classificazione dei dati e creazione di criteri di utilizzo dei dati tramite [!DNL Experience Platform] interfaccia utente e [!DNL Policy Service] API.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Gestire i criteri di utilizzo dei dati nell’interfaccia utente | È ora possibile gestire i criteri di utilizzo dei dati all’interno di **Criteri** nell&#39;area di lavoro [!DNL Experience Platform] Interfaccia utente. Consulta la sezione [guida utente di policy](../../data-governance/policies/user-guide.md) per ulteriori informazioni. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni, consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md).


## Destinazioni {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Real-time CDP ora supporta l’attivazione dei dati a oltre cinquanta [!DNL Experience Cloud Launch] estensioni, abilitazione di analytics, personalizzazione e altri casi d’uso. Vedi sotto per i dettagli:

| Documentazione | Descrizione |
|--- | ---|
| [Tipi di destinazione e categorie](../../destinations/destination-types.md) | Questo articolo spiega la differenza tra connessioni ed estensioni nell&#39;interfaccia Real-time CDP e consiglia quando utilizzare ciascuna di queste destinazioni. |
| [Estensioni Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Questa pagina spiega cosa [!DNL Launch] le estensioni sono elencate, elenca i casi d’uso per utilizzarle e i collegamenti alla documentazione per ogni [!DNL Launch] estensione in Real-time CDP. |

Per ulteriori informazioni, consulta la sezione [Panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente per aiutarti a gestire queste richieste di dati dai clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di accesso a dati personali possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando esegui richieste di privacy nell’API, la `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia utente | Ora puoi specificare diversi tipi di namespace nel Generatore di richieste nel [!DNL Privacy Service] Interfaccia utente. Consulta la sezione [guida utente](../../privacy-service/ui/user-guide.md) per ulteriori informazioni. |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

Problemi noti

* Nessuna

Per ulteriori informazioni [!DNL Privacy Service], si prega di iniziare leggendo il [Panoramica di Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto API e interfaccia utente per i database | Nuovi connettori sorgente per [!DNL Apache Spark] (su HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (su HDInsights) e [!DNL Phoenix]. |
| Supporto API e interfaccia utente per applicazioni basate su pagamenti | Nuovi connettori sorgente per [!DNL PayPal]. |
| Supporto API e interfaccia utente per applicazioni basate su protocolli | Nuovi connettori sorgente per [!DNL Generic OData]. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
