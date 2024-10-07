---
title: Informazioni SQL
description: Scopri i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare un dashboard di SQL Insights con Data Distiller. Scopri in che modo la funzionalità SQL Insights in Data Distiller può migliorare la trasparenza e ottenere informazioni operative attraverso diverse dimensioni, come profili, tipi di pubblico, campagne, percorsi, autorizzazioni e consenso.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: 4e78a7983fba492ded866a8f1fc6f98e20510b2b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Informazioni SQL

Con SQL Insights di Data Distiller puoi creare modelli di dati di reporting personalizzati per estrarre informazioni più approfondite, ottimizzare le strategie e adattare le analisi per soddisfare esigenze aziendali specifiche. Utilizza la funzionalità SQL Insights per migliorare la trasparenza e ottenere informazioni operative dai dati Adobe Experience Platform in dimensioni quali profili, tipi di pubblico, campagne, percorsi, autorizzazioni e consenso. Questa funzionalità offre una soluzione versatile e adattiva per adattare i modelli di dati di reporting della tua organizzazione alle tue esigenze aziendali specifiche.

Per [visualizzare SQL Insights](../../../dashboards/data-distiller/sql-insights/overview.md) puoi utilizzare la [modalità query pro](../../../dashboards/data-distiller/query-pro-mode/overview.md) per eseguire analisi complesse con query SQL personalizzate e trasformare i tuoi dati in grafici facilmente interpretabili. Utilizza la modalità query pro per creare informazioni e visualizzazioni personalizzate sulle dashboard e soddisfare i tipi di pubblico tecnici e non, scaricando le informazioni come file CSV.

Questo documento descrive i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare un dashboard di SQL Insights con Data Distiller.

## Prerequisiti

Questa esercitazione utilizza dashboard definite dall’utente per visualizzare i dati dal modello dati personalizzato nell’interfaccia utente di Platform. Per ulteriori informazioni su questa funzione, consulta la [documentazione delle dashboard definite dall&#39;utente](../../../dashboards/user-defined-dashboards.md).

## Introduzione

Lo SKU di Data Distiller è necessario per creare un modello dati personalizzato per le informazioni di reporting ed estendere i modelli dati di Real-Time CDP che contengono dati Platform arricchiti. Consulta la documentazione [package](../../packaging.md), [guardrail](../../guardrails.md#query-accelerated-store) e [licensing](../../data-distiller/license-usage.md) relativa allo SKU di Data Distiller. Se non disponi dello SKU di Data Distiller, contatta il rappresentante dell’assistenza clienti Adobe per ulteriori informazioni.

## Casi di utilizzo di SQL Insights {#use-cases}

Di seguito sono riportati alcuni casi d’uso comuni che possono essere risolti in modo efficace tramite SQL Insights in Data Distiller.

### Trasparenza dell’utilizzo di profili e pubblico {#usage-transparency}

**Sfida:** come suddividere gli indicatori prestazioni chiave (KPI, Key Performance Indicators) in base a criteri specifici quali business unit, stato di fedeltà o valore del ciclo di vita del cliente (CLTV, Customer Lifetime Value).

**Soluzione SQL Insights:** Data Distiller abilita l&#39;estensione dei modelli di dati di reporting in Adobe Experience Platform, facilitando [l&#39;aggiunta di attributi di profilo personalizzati come CLTV](../../use-cases/customer-lifetime-value.md) o lo stato di fedeltà.

### Tracciamento delle anomalie del consenso {#consent-anomaly-tracking}

**Sfida:** come applicare i rapporti di sovrapposizione del pubblico e di dimensione della linea di tendenza agli attributi di consenso personalizzati per canali come e-mail, SMS e telefono.

**Soluzione SQL Insights:** il modello dati di reporting può essere esteso per tenere traccia delle modifiche nelle preferenze di consenso nel tempo. Ciò comporta la creazione di tabelle di fact e dimensioni aggiuntive per impostare le preferenze di consenso e pianificare [l&#39;aggiornamento incrementale dei dati](../../key-concepts/incremental-load.md).

### Ottimizzare la strategia di segmentazione del pubblico {#optimize-audience-segmentation-strategy}

**Sfida:** come integrare i punteggi di propensione generati dal modello di apprendimento automatico (ML) nei rapporti KPI del pubblico.

**Soluzione SQL Insights:** Data Distiller consente di includere [punteggi di tendenza dai modelli ML personalizzati](../../use-cases/propensity-score.md), semplificando il calcolo dei punteggi aggregati a livello di pubblico. Questi dati possono quindi essere segnalati insieme ai KPI standard.

### Espansione del pubblico {#audience-expansion}

**Sfida:** come acquisire più di semplici conteggi di profilo nei rapporti di sovrapposizione del pubblico e ottenere ulteriori dati demografici o preferenze per guidare le strategie di espansione del pubblico.

**Soluzione SQL Insights:** estendendo il modello dati di reporting, gli utenti possono incorporare attributi di profilo aggiuntivi, arricchendo il rapporto di sovrapposizione del pubblico con i dati demografici e le preferenze pertinenti.

## Funzionalità chiave per la generazione di SQL Insights {#key-capabilities}

Nell&#39;illustrazione seguente sono illustrate diverse funzionalità essenziali per la generazione di SQL Insights. Queste funzionalità includono:

1. **Visualizzazioni dati:** incorporazione di elementi visivi quali tendenze e grafici a barre per una visualizzazione completa delle tendenze dei dati.
1. **Authoring del dashboard:** abilitazione della creazione di dashboard personalizzati adatti a casi d&#39;uso specifici, per un&#39;esperienza di analisi più personalizzata e mirata.
1. **Modellazione dati SQL flessibile:** Utilizzare un approccio di modellazione dati SQL versatile che consente agli utenti di combinare e manipolare facilmente set di dati diversi, migliorando l&#39;adattabilità e il livello di dettaglio analitico.
1. **Archivio accelerato:** implementazione di un meccanismo di archiviazione accelerata per fornire in modo efficiente informazioni aggregate tramite SQL, garantendo un accesso rapido e semplificato a informazioni importanti.
1. **Connettività BI:** integrazione semplificata con i più diffusi strumenti di Business Intelligence (BI), tra cui Power BI, Tableau, Looker e Apache Superset. Questa connettività garantisce la compatibilità con diversi ambienti BI, offrendo agli utenti la flessibilità di utilizzare lo strumento desiderato per l’analisi approfondita e il reporting.

![Rappresentazioni visive delle funzionalità chiave di Data Distiller SQL Insights.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Passaggi per creare SQL Insights {#steps-to-create}

Per sviluppare un dashboard di SQL Insights all’interno di Data Distiller, segui le istruzioni dettagliate riportate di seguito.

1. **Esplorazione di query ad hoc:** Eseguire query ad hoc `SELECT` per esplorare i dati non elaborati nel data lake. Ciò consente di eseguire al volo analisi dei dati esplorative per sperimentare e convalidare i dati laddove i risultati delle query non sono memorizzati nel data lake.
1. **Utilizzo query batch:** Utilizzare query batch per [creare processi pianificati](../../api/scheduled-queries.md#create-a-new-scheduled-query) per la generazione di tabelle di aggregazione approfondimenti, garantendo un approccio sistematico e automatizzato all&#39;elaborazione dei dati. Le query batch eseguono `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` query per pulire, modellare, manipolare e arricchire i dati. I risultati di queste query vengono memorizzati nel data lake.
1. **Caricamento delle informazioni aggregate:** Carica le informazioni aggregate generate nell&#39;archivio accelerato e utilizza SQL per testare le query e garantire l&#39;accuratezza e l&#39;efficienza del recupero dei dati. Per informazioni su come [eseguire query senza stato nell&#39;archivio accelerato](../../api/accelerated-queries.md), consulta la documentazione.
1. **Accesso e integrazione:** Accesso senza problemi alle informazioni archiviate nell&#39;archivio accelerato tramite l&#39;integrazione con Adobe Experience Platform [Dashboard definiti dall&#39;utente](../../../dashboards/user-defined-dashboards.md) o altri strumenti di Business Intelligence preferiti (BI). Queste integrazioni con client di terze parti facilitano un’esperienza coerente e intuitiva per gli utenti.

![Un&#39;infografica che illustra i quattro passaggi per SQL Insights in Data Distiller.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Passaggi successivi

Una volta letto questo documento, potrai comprendere meglio i casi d’uso, le funzionalità essenziali e i passaggi necessari per sviluppare un dashboard di SQL Insights con Data Distiller. Per ulteriori informazioni sulla creazione di modelli dati per la generazione di rapporti personalizzati, consulta la [guida al modello dati approfondimenti per la generazione di rapporti](./reporting-insights-data-model.md).
