---
title: Approfondimenti personalizzabili
description: Scopri i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare una dashboard di approfondimenti personalizzabile con Data Distiller. Scopri in che modo la funzionalità Approfondimenti personalizzabili di Data Distiller può migliorare la trasparenza e ottenere informazioni operative tra diverse dimensioni, come profili, tipi di pubblico, campagne, percorsi, autorizzazioni e consenso.
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Approfondimenti personalizzabili

Con Registri personalizzabili di Data Distiller puoi creare modelli di dati per la generazione di rapporti personalizzati, per estrarre informazioni più approfondite, ottimizzare le strategie e adattare le analisi per soddisfare esigenze aziendali specifiche. Utilizza la funzionalità Approfondimenti personalizzabili per migliorare la trasparenza e ottenere informazioni operative dai dati Adobe Experience Platform su dimensioni quali profili, tipi di pubblico, campagne, percorsi, autorizzazioni e consenso. Questa funzionalità offre una soluzione versatile e adattiva per adattare i modelli di dati di reporting della tua organizzazione alle tue esigenze aziendali specifiche.

Questo documento descrive i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare una dashboard di approfondimenti personalizzabile con Data Distiller.

## Prerequisiti

Questa esercitazione utilizza dashboard definite dall’utente per visualizzare i dati dal modello dati personalizzato nell’interfaccia utente di Platform. Consulta la [documentazione delle dashboard definite dall&#39;utente](../../../dashboards/user-defined-dashboards.md) per ulteriori informazioni su questa funzione.

## Introduzione

Lo SKU di Data Distiller è necessario per creare un modello dati personalizzato per le informazioni di reporting ed estendere i modelli dati di Real-Time CDP che contengono dati Platform arricchiti. Consulta la [imballaggio](../../packaging.md), [guardrail](../../guardrails.md#query-accelerated-store), e  [licenza](../../data-distiller/license-usage.md) documentazione relativa allo SKU di Data Distiller. Se non disponi dello SKU di Data Distiller, contatta il rappresentante dell’assistenza clienti Adobe per ulteriori informazioni.

## Casi di utilizzo di Insights personalizzabili {#use-cases}

Di seguito sono riportati alcuni casi d’uso comuni che possono essere risolti in modo efficace tramite Approfondimenti personalizzabili in Data Distiller.

### Trasparenza dell’utilizzo di profili e pubblico {#usage-transparency}

**Sfida:** Come suddividere gli indicatori di prestazioni chiave (KPI, Key Performance Indicators) in base a criteri specifici quali business unit, stato di fedeltà o valore del ciclo di vita del cliente (CLTV, Customer Lifetime Value).

**Soluzione di approfondimenti personalizzabile:** Data Distiller consente l’estensione dei modelli di dati per la generazione di rapporti in Adobe Experience Platform, facilitando [l’aggiunta di attributi di profilo personalizzati, come CLTV](../../use-cases/customer-lifetime-value.md) o allo stato di fedeltà.

### Tracciamento delle anomalie del consenso {#consent-anomaly-tracking}

**Sfida:** Come applicare i rapporti di sovrapposizione del pubblico e di dimensione della linea di tendenza agli attributi di consenso personalizzati per canali come e-mail, SMS e telefonici.

**Soluzione di approfondimenti personalizzabile:** Il modello per i dati di reporting può essere esteso per tenere traccia delle modifiche nelle preferenze di consenso nel tempo. Ciò comporta la creazione di tabelle di fatti e dimensioni aggiuntive per le preferenze e la pianificazione del consenso delle tendenze [aggiornamento dati incrementale](../../key-concepts/incremental-load.md).

### Ottimizzare la strategia di segmentazione del pubblico {#optimize-audience-segmentation-strategy}

**Sfida:** Come integrare i punteggi di propensione generati dal modello di apprendimento automatico (ML) nei rapporti KPI per il pubblico.

**Soluzione di approfondimenti personalizzabile:** Data Distiller consente di includere [punteggi di propensione da modelli ML personalizzati](../../use-cases/propensity-score.md), facilitando il calcolo dei punteggi aggregati a livello di pubblico. Questi dati possono quindi essere segnalati insieme ai KPI standard.

### Espansione del pubblico {#audience-expansion}

**Sfida:** Come acquisire più di semplici conteggi di profilo nei rapporti di sovrapposizione del pubblico e ottenere ulteriori dati o preferenze demografiche per guidare le strategie di espansione del pubblico.

**Soluzione di approfondimenti personalizzabile:** Estendendo il modello dati di reporting, gli utenti possono incorporare attributi di profilo aggiuntivi, arricchendo il rapporto di sovrapposizione del pubblico con dati demografici e preferenze pertinenti.

## Funzionalità chiave per generare Approfondimenti personalizzabili {#key-capabilities}

L’illustrazione seguente evidenzia diverse funzionalità essenziali per la generazione di Approfondimenti personalizzabili. Queste funzionalità includono:

1. **Visualizzazioni dati:** Incorporazione di elementi visivi quali tendenze e grafici a barre per una visualizzazione completa delle tendenze dei dati.
1. **Creazione dashboard:** Abilitazione della creazione di dashboard personalizzati personalizzati personalizzati adatti a casi d’uso specifici, per un’esperienza di analisi più personalizzata e mirata.
1. **Modellazione dati SQL flessibile:** Utilizza un approccio versatile alla modellazione dei dati SQL che consente agli utenti di combinare e manipolare facilmente diversi set di dati, migliorando l’adattabilità e la profondità analitica.
1. **Archiviazione accelerata:** Implementazione di un meccanismo di archiviazione accelerata per fornire in modo efficiente informazioni aggregate tramite SQL, garantendo un accesso semplificato e rapido a informazioni preziose.
1. **Connettività BI:** Facilitare l’integrazione diretta con i più diffusi strumenti di Business Intelligence (BI), tra cui Power BI, Tableau, Looker e Apache Superset. Questa connettività garantisce la compatibilità con diversi ambienti BI, offrendo agli utenti la flessibilità di utilizzare lo strumento desiderato per l’analisi approfondita e il reporting.

![Rappresentazioni visive delle funzionalità chiave di Informazioni personalizzabili di Data Distiller.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Passaggi per creare Approfondimenti personalizzabili {#steps-to-create}

Per sviluppare una dashboard di Approfondimenti personalizzabili in Data Distiller, segui le istruzioni dettagliate riportate di seguito.

1. **Esplorazione di query ad hoc:** Iniziare eseguendo ad hoc `SELECT` query per esplorare i dati non elaborati nel data lake. Ciò consente di eseguire al volo analisi dei dati esplorative per sperimentare e convalidare i dati laddove i risultati delle query non sono memorizzati nel data lake.
1. **Utilizzo query batch:** Utilizzare le query batch per [crea processi pianificati](../../api/scheduled-queries.md#create-a-new-scheduled-query) per generare tabelle aggregate di insights, garantendo un approccio sistematico e automatizzato all’elaborazione dei dati. Esecuzione di query batch `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` query per pulire, modellare, manipolare e arricchire i dati. I risultati di queste query vengono memorizzati nel data lake.
1. **Caricamento di informazioni aggregate:** Carica le informazioni aggregate generate nell’archivio accelerato e utilizza SQL per testare le query e garantire l’accuratezza e l’efficienza del recupero dei dati. Per scoprire come [eseguire query senza stato nell&#39;archivio accelerato](../../api/accelerated-queries.md), consulta la documentazione.
1. **Accesso e integrazione:** Accedi senza problemi alle informazioni memorizzate nel negozio accelerato tramite l’integrazione con Adobe Experience Platform [Dashboard definiti dall&#39;utente](../../../dashboards/user-defined-dashboards.md) o altri strumenti di Business Intelligence preferiti (BI). Queste integrazioni con client di terze parti facilitano un’esperienza coerente e intuitiva per gli utenti.

![Un’infografica che illustra i quattro passaggi per personalizzare gli approfondimenti in Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Passaggi successivi

Una volta letto questo documento, potrai comprendere meglio i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare una dashboard di approfondimenti personalizzabile con Data Distiller. Per ulteriori informazioni sulla creazione di modelli di dati per reporting personalizzati, consulta la sezione [guida al modello dati per reporting insights](./reporting-insights-data-model.md).
