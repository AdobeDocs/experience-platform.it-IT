---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione di Experience Platform, 8 aprile 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 1e2299980572116d589e7164dd20e171433a284a

---


# Note sulla versione di Adobe Experience Platform

## Data di rilascio: 8 aprile 2020

## Governance dei dati

Adobe Experience Platform Data Governance è una serie di strategie e tecnologie utilizzate per gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all&#39;utilizzo dei dati. Essa svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, line-up di dati, etichettatura dell’utilizzo dei dati, criteri di accesso ai dati e controllo dell’accesso ai dati per le azioni di marketing.

Per iniziare a utilizzare la gestione dei dati è necessario conoscere a fondo le normative, gli obblighi contrattuali e le politiche aziendali applicabili ai dati dei clienti. Da qui, i dati possono essere classificati applicando le etichette di utilizzo dei dati appropriate e il loro utilizzo può essere controllato tramite la definizione di criteri di utilizzo dei dati.

Il framework DULE semplifica e semplifica il processo di classificazione dei dati e creazione di criteri di utilizzo dei dati tramite l’interfaccia utente della piattaforma Experience e l’API del servizio DULE Policy.

### Nuove funzionalità

| Funzione | Descrizione |
| -----------| ---------- |
| Gestione dei criteri di utilizzo dei dati nell’interfaccia utente | I criteri di utilizzo dei dati possono ora essere gestiti nell&#39;area di lavoro _Criteri_ dell&#39;interfaccia utente della piattaforma Experience. Per ulteriori informazioni, consultate la guida [utente ai](../../data-governance/policies/user-guide.md) criteri. |

**Problemi noti**

* None.

Per ulteriori informazioni, consulta la panoramica sulla governance dei [dati](../../data-governance/home.md).

## Servizi intelligenti

I servizi intelligenti consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell&#39;intelligenza artificiale e dell&#39;apprendimento automatico nei casi di utilizzo dell&#39;esperienza cliente. Questo consente agli analisti di marketing di impostare previsioni specifiche per le esigenze di un&#39;azienda utilizzando configurazioni a livello di business, senza bisogno di conoscenze scientifiche. Inoltre, i professionisti del marketing possono attivare le previsioni in Adobe Experience Cloud, Adobe Experience Platform e applicazioni di terze parti.

**Funzionalità chiave**

| Funzione | Descrizione |
|---|---|
| AI cliente | L&#39;AI del cliente fornisce agli esperti di marketing il potere di generare previsioni dei clienti a livello individuale con spiegazioni. Con l&#39;aiuto di fattori influenti, l&#39;intelligenza artificiale del cliente può dirvi cosa è probabile fare e perché. Inoltre, gli esperti di marketing possono trarre vantaggio dalle previsioni e dalle informazioni dell&#39;AI cliente per personalizzare l&#39;esperienza dei clienti, servendo le offerte e i messaggi più appropriati. |
| Attribuzione AI | L&#39;AI di attribuzione è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a determinati risultati. Con Attribution AI, gli addetti al marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l&#39;impatto di ogni singola interazione con i clienti in ogni fase dei viaggi dei clienti. |

**Problemi noti**

* Nessun problema noto al momento.

Per maggiori informazioni sui servizi intelligenti e sui servizi offerti, consulta la panoramica [sui servizi](../../intelligent-services/home.md)intelligenti.

## Servizio Privacy

Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta. Il servizio Adobe Experience Platform Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Il servizio Privacy consente di inviare richieste per l&#39;accesso e l&#39;eliminazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatizzata alle normative sulla privacy legali e organizzative.

**Nuove funzionalità**

| Funzione | Descrizione |
| --- | --- |
| Supporto PDPA | Le richieste di privacy possono ora essere create e monitorate in base al Personal Data Protection Act (PDPA) in Thailandia. Quando si effettuano richieste di privacy nell&#39;API, l&#39; `regulation` array accetta il valore &quot;pdpa_tha&quot;. |
| Tipi di namespace nell’interfaccia | È ora possibile specificare diversi tipi di spazio nomi in Request Builder nell&#39;interfaccia utente del servizio per la privacy. Per ulteriori informazioni, consultate la guida [](../../privacy-service/ui/user-guide.md) utente. |
| Obsoleto endpoint precedente | Il vecchio endpoint API (`data/privacy/gdpr`) è stato dichiarato obsoleto. |

Problemi noti

* None

Per ulteriori informazioni sul servizio Privacy, consultare la panoramica [del servizio](../../privacy-service/home.md)Privacy.

## Origini

Adobe Experience Platform è in grado di acquisire dati da origini esterne e allo stesso tempo di strutturarli, etichettarli e ottimizzarli tramite i servizi della piattaforma. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

### Nuove funzionalità

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto API e interfaccia utente per i database | Nuovi connettori sorgente per Apache Spark (su HDInsights), Azure Synapse Analytics, Azure Table Storage, Hive (su HDInsights) e Phoenix. |
| Supporto API e interfaccia utente per applicazioni basate su pagamenti | Nuovi connettori sorgente per PayPal. |
| Supporto API e interfaccia utente per applicazioni basate su protocolli | Nuovi connettori sorgente per OData generico. |

### Problemi noti

* None

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../source-connectors/home.md).