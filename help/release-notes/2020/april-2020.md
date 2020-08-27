---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform 8 aprile 2020'
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 5%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 8 aprile 2020**

Nuove funzioni in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aggiornamenti alle funzioni esistenti:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinazioni]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] consente agli analisti e ai professionisti del marketing di sfruttare la potenza dell&#39;intelligenza artificiale e dell&#39;apprendimento automatico nei casi di utilizzo dell&#39;esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un&#39;azienda utilizzando configurazioni a livello di business, senza bisogno di conoscenze scientifiche. Inoltre, i professionisti del marketing possono attivare le previsioni nelle applicazioni di Adobe Experience Cloud, Adobe Experience Platform e di terze parti.

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] fornisce agli esperti di marketing il potere di generare previsioni dei clienti a livello individuale con spiegazioni. Con l&#39;aiuto di fattori influenti, [!DNL Customer AI] puoi sapere cosa è probabile che faccia un cliente e perché. Inoltre, gli esperti di marketing possono trarre vantaggio da [!DNL Customer AI] previsioni e informazioni per personalizzare l&#39;esperienza dei clienti servendo le offerte e i messaggi più appropriati. |
| [!DNL Attribution AI] | [!DNL Attribution AI] è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a risultati specifici. Grazie a [!DNL Attribution AI]questa soluzione, gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l&#39;impatto di ogni singola interazione con i clienti in ogni fase dei viaggi dei clienti. |

**Problemi noti**

* Nessun problema noto al momento.

Per ulteriori informazioni su [!DNL Intelligent Services] cosa offre, consulta la panoramica [sui servizi](../../intelligent-services/home.md)intelligenti.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

Standardizzazione e interoperabilità sono concetti chiave alla base di [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

XDM è una specifica documentata pubblicamente progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione che comunica con i servizi di Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati relativi all&#39;esperienza dei clienti possono essere incorporati in una rappresentazione comune, fornendo informazioni approfondite in modo più rapido e integrato. Puoi ricavare informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Informazioni di visualizzazione alternative automatiche | Applica [!DNL Schema Registry] automaticamente i valori personalizzati di titolo e descrizione configurati nel `alternateDisplayInfo` descrittore. |
| Limitazioni per i campi scalari | In un singolo schema [!DNL Schema Registry] non sono consentiti più di 6000 campi scalari. |
| Revisione delle prestazioni | Il [!DNL Schema Registry] progetto è stato modificato per soddisfare le esigenze di [!DNL Experience Platform] miglioramento. |

**Correzioni di bug**

* È stato aggiornato XDM in XED convertito per supportare un formato XED più pulito per i campi URI nidificati in XDM standard.

**Problemi noti**

* Noto

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati. Esso svolge un ruolo chiave a vari livelli, [!DNL Experience Platform] tra cui catalogazione, linea di dati, etichettatura dell&#39;utilizzo dei dati, criteri di accesso ai dati e controllo dell&#39;accesso ai dati per le azioni di marketing.

Per iniziare a utilizzare la gestione dei dati è necessario conoscere a fondo le normative, gli obblighi contrattuali e le politiche aziendali applicabili ai dati dei clienti. Da qui, i dati possono essere classificati applicando le etichette di utilizzo dei dati appropriate e il loro utilizzo può essere controllato tramite la definizione di criteri di utilizzo dei dati.

Il framework DULE semplifica e semplifica il processo di classificazione dei dati e creazione di criteri di utilizzo dei dati tramite l&#39;interfaccia [!DNL Experience Platform] utente e l&#39; [!DNL Policy Service] API DULE.

**Nuove funzionalità**

| Funzione | Descrizione |
| -----------| ---------- |
| Gestione dei criteri di utilizzo dei dati nell’interfaccia utente | I criteri di utilizzo dei dati possono ora essere gestiti nell&#39;area di lavoro _Criteri_ dell&#39; [!DNL Experience Platform] interfaccia utente. Per ulteriori informazioni, consultate la guida [utente ai](../../data-governance/policies/user-guide.md) criteri. |

**Problemi noti**

* Nessuna.

Per ulteriori informazioni, consulta la panoramica sulla governance dei [dati](../../data-governance/home.md).


## Destinazioni {#destinations}

In [Adobe Real-time Customer Data Platform](../../rtcdp/overview.md), le destinazioni sono integrazioni precostruite con piattaforme di destinazione che attivano i dati a tali partner in modo semplice.

**Nuove destinazioni**

 CDP in tempo reale supporta ora l&#39;attivazione dei dati a oltre cinquanta [!DNL Experience Cloud Launch] estensioni, consentendo analisi, personalizzazione e altri casi di utilizzo. Per ulteriori informazioni, vedere di seguito:

| Documentazione | Descrizione |
|--- | ---|
| [Tipi e categorie di destinazione](/help/rtcdp/destinations/destination-types.md) | Questo articolo spiega la differenza tra connessioni ed estensioni nell&#39;interfaccia CDP in tempo reale del Adobe  e consiglia quando utilizzare ciascuna di queste destinazioni. |
| [Estensioni Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | In questa pagina sono illustrate [!DNL Launch] le estensioni, sono elencati i casi di utilizzo per utilizzarle e sono disponibili collegamenti alla documentazione per ogni [!DNL Launch] estensione nel CDP in tempo reale  Adobe. |

Per ulteriori informazioni, consulta la panoramica [](/help/rtcdp/destinations/destinations-overview.md)Destinazioni.

## [!DNL Privacy Service] {#privacy}

Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Con [!DNL Privacy Service]questa opzione puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative sulla privacy legali e organizzative.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di privacy possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39; `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia | È ora possibile specificare diversi tipi di spazio nomi nel Generatore di richieste nell&#39; [!DNL Privacy Service] interfaccia utente. Per ulteriori informazioni, consultate la guida [](../../privacy-service/ui/user-guide.md) utente. |
| Obsoleto endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

Problemi noti

* Nessuna

Per ulteriori informazioni su [!DNL Privacy Service]questo argomento, leggete la panoramica [Privacy Service](../../privacy-service/home.md).

## Origini {#sources}

Adobe Experience Platform è in grado di acquisire dati da origini esterne e di strutturarli, etichettarli e ottimizzarli utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni  Adobe, storage basato su cloud, software di terze parti e il sistema CRM in uso.

[!DNL Experience Platform] fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto API e interfaccia utente per i database | Nuovi connettori sorgente per [!DNL Apache Spark] (su HDInsight), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (su HDInsight) e [!DNL Phoenix]. |
| Supporto API e interfaccia utente per applicazioni basate su pagamenti | Nuovi connettori sorgente per [!DNL PayPal]. |
| Supporto API e interfaccia utente per applicazioni basate su protocolli | Nuovi connettori sorgente per [!DNL Generic OData]. |

**Problemi noti**

* Nessuna

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
