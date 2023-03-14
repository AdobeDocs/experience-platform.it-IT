---
title: Note sulla versione di Adobe Experience Platform - Aprile 2020
description: Note sulla versione di aprile 2020 per Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: note sulla versione;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 10%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 8 aprile 2020**

Nuove funzioni di Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Governance dei dati](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] consenti agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale senza la necessità di competenze in materia di data science. Inoltre, i professionisti del marketing possono attivare le previsioni in applicazioni Adobe Experience Cloud, Adobe Experience Platform e di terze parti.

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] offre agli esperti di marketing la possibilità di generare previsioni sui clienti a livello individuale con spiegazioni. Con l&#39;aiuto di fattori di influenza, [!DNL Customer AI] può dirti cosa potrebbe fare un cliente e perché. Inoltre, gli addetti al marketing possono trarre vantaggio da [!DNL Customer AI] previsioni e informazioni utili per personalizzare le esperienze dei clienti fornendo le offerte e i messaggi più appropriati. |
| [!DNL Attribution AI] | [!DNL Attribution AI] è un servizio di attribuzione algoritmica multicanale che calcola l’influenza e l’impatto incrementale delle interazioni dei clienti rispetto a risultati specifici. Con [!DNL Attribution AI], gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l’impatto di ogni singola interazione con i clienti in ogni fase del percorso del cliente. |

**Problemi noti**

* Nessun problema noto.

Per ulteriori informazioni su [!DNL Intelligent Services] e ciò che ha da offrire, consulta [Panoramica di Intelligent Services](../../intelligent-services/home.md).

## Sistema [!DNL Experience Data Model] (XDM)  {#xdm}

La standardizzazione e l&#39;interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da Adobe, è un tentativo di standardizzare i dati sull’esperienza del cliente e definire schemi per la gestione della customer experience.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune che fornisce informazioni in modo più veloce e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Informazioni visualizzazione alternativa automatica | Il [!DNL Schema Registry] applica automaticamente i valori personalizzati del titolo e della descrizione configurati nella `alternateDisplayInfo` descrittore. |
| Limitazioni dei campi scalari | Il [!DNL Schema Registry] non consente più di 6000 campi scalari in un singolo schema. |
| Revisione delle prestazioni | Il [!DNL Schema Registry] è stato revisionato per eseguire e soddisfare le richieste di [!DNL Experience Platform] meglio. |

**Correzioni di bug**

* XDM è stato aggiornato a XED convertito per supportare un formato XED più pulito per i campi URI nidificati in XDM standard.

**Problemi noti**

* Noto

## Governance dei dati {#governance}

La governance dei dati di Adobe Experience Platform è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave in [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo degli accessi ai dati per le azioni di marketing.

La guida introduttiva alla governance dei dati richiede una comprensione approfondita delle normative, degli obblighi contrattuali e delle politiche aziendali applicabili ai dati dei clienti. Da lì, i dati possono essere classificati applicando le etichette di utilizzo dei dati appropriate e il loro utilizzo può essere controllato tramite la definizione di criteri di utilizzo dei dati.

Il framework per la governance dei dati semplifica e snellisce il processo di categorizzazione dei dati e di creazione di policy di utilizzo dei dati tramite [!DNL Experience Platform] e [!DNL Policy Service] API.

**Nuove funzioni**

| Funzione | Descrizione |
| -----------| ---------- |
| Gestire i criteri di utilizzo dei dati nell’interfaccia utente | I criteri di utilizzo dei dati possono ora essere gestiti all’interno di **Criteri** area di lavoro in [!DNL Experience Platform] UI. Consulta la [guida utente dei criteri](../../data-governance/policies/user-guide.md) per ulteriori informazioni. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md).


## Destinazioni {#destinations}

In entrata [Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni predefinite con piattaforme di destinazione che attivano i dati per tali partner in modo semplice.

**Nuove destinazioni**

Real-Time CDP ora supporta l’attivazione dei dati fino a oltre cinquanta [!DNL Experience Cloud Launch] estensioni, abilitazione di analytics, personalizzazione e altri casi d’uso. Per ulteriori informazioni, consulta:

| Documentazione | Descrizione |
|--- | ---|
| [Tipi e categorie di destinazione](../../destinations/destination-types.md) | Questo articolo spiega la differenza tra connessioni ed estensioni nell&#39;interfaccia di Real-Time CDP e consiglia quando utilizzare ciascuna di queste destinazioni. |
| [Estensioni Experience Platform Launch](../../destinations/catalog/launch-extensions/overview.md) | Questa pagina spiega cosa [!DNL Launch] le estensioni sono, elenca i casi di utilizzo per ciascuna di esse e i collegamenti alla relativa documentazione [!DNL Launch] in Real-Time CDP. |

Per ulteriori informazioni, vedere [Panoramica sulle destinazioni](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Nuovi regolamenti legali e organizzativi danno agli utenti il diritto di accedere ai propri dati o di cancellarli dagli archivi dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di dati dei clienti. Con [!DNL Privacy Service], puoi inviare richieste di accesso e cancellazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di accesso ai dati personali possono ora essere create e monitorate in base alla legge sulla protezione dei dati personali (PDPA) in Thailandia. Quando effettui richieste di accesso a dati personali nell’API, il `regulation` l’array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di spazio dei nomi nell’interfaccia utente | Ora puoi specificare diversi tipi di spazio dei nomi nel Generatore di richieste in [!DNL Privacy Service] UI. Consulta la [guida utente](../../privacy-service/ui/user-guide.md) per ulteriori informazioni. |
| Obsolescenza endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

Problemi noti

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service], inizia leggendo il [Panoramica di Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando [!DNL Platform] servizi. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

[!DNL Experience Platform] fornisce un’API RESTful e un’interfaccia utente interattiva che consente di configurare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Nuove funzioni**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto API e interfaccia utente per i database | Nuovi connettori sorgente per [!DNL Apache Spark] (su HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (su HDInsights), e [!DNL Phoenix]. |
| Supporto API e interfaccia utente per applicazioni basate su pagamenti | Nuovi connettori sorgente per [!DNL PayPal]. |
| Supporto di API e interfaccia utente per applicazioni basate su protocolli | Nuovi connettori sorgente per [!DNL Generic OData]. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
