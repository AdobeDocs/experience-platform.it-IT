---
title: Flusso di lavoro end-to-end per l’arricchimento della pipeline di dati AI/ML
description: Utilizza i notebook dell’ambiente di apprendimento automatico basato su cloud per creare un corso di formazione e assegnare un punteggio a un modello di propensione che prevede le conversioni degli abbonamenti dai dati di Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Flusso di lavoro end-to-end per l’arricchimento della pipeline dati AI/ML

Utilizza Data Distiller per arricchire le pipeline di apprendimento automatico con dati di alto valore sull’esperienza del cliente che sono stati raccolti e curati in Adobe Experience Platform.

Questo documento fornisce una serie di notebook per ambienti di apprendimento automatico basati su cloud che illustrano un flusso di lavoro end-to-end. Il flusso di lavoro utilizza gli strumenti di apprendimento automatico preferiti per creare modelli di dati personalizzati che supportano i casi di utilizzo di marketing con i dati di Experience Platform.

Questo flusso di lavoro richiede l’utilizzo di [!DNL Python] notebook negli ambienti di apprendimento automatico. Istruzioni per iniziare a usare questi [!DNL Python] I notebook sono inclusi nei rispettivi file readme.

Prima di continuare con questa guida, segui i passaggi descritti in [Panoramica delle pipeline delle funzioni AI/ML](./overview.md) per abilitare l’uso dei notebook Python di esempio utilizzati in questo caso d’uso della pipeline di funzioni AI/ML.

## Notebook dell’ambiente di apprendimento automatico cloud {#cmle-notebooks}

Il flusso di lavoro end-to-end può essere suddiviso in tre ampie fasi in base ai servizi utilizzati per implementare il flusso di lavoro.

- L’esplorazione e la preparazione iniziali dei dati di Platform si basano sui servizi di Platform.
- L’apprendimento e il punteggio dei modelli sfruttano gli strumenti nell’ambiente ML basato su cloud. Le scelte comuni per le piattaforme ML includono: Databricks ML, AWS Sagemaker, DataRobot e così via.
- L’inserimento di punteggi nuovamente in Platform e qualsiasi creazione e attivazione di pubblico basata su codice basata su tali punteggi si baserebbero nuovamente sui servizi di Platform.

Tuttavia, tutte queste fasi possono essere eseguite in uno o più notebook dall’ambiente di apprendimento automatico senza che l’utente debba cambiare contesto tra Platform e i relativi strumenti di apprendimento automatico basati su cloud.

Le fasi tipiche di questo flusso end-to-end sono state suddivise in una serie di notebook modulari che, nel loro insieme, dimostrano le fasi di un tipico progetto di apprendimento automatico che coinvolge i dati di Platform. In questo modo è più facile utilizzare i notebook come riferimento per l&#39;implementazione di attività specifiche, nonché selezionare e adattare il codice dai relativi notebook per implementare un caso d&#39;uso reale. In pratica, un data scientist può preparare un singolo blocco appunti che implementa la pipeline end-to-end per il proprio progetto di ML. In alternativa, un data scientist può semplicemente adattare il codice di esempio per eseguire query sui dati di Platform e renderli disponibili nel proprio ambiente di apprendimento automatico prima di continuare il progetto utilizza funzionalità basate sull’interfaccia utente nella propria piattaforma di apprendimento automatico.

Di seguito sono brevemente descritti i blocchi appunti di esempio inclusi nell’archivio collegato. La documentazione dettagliata di ciascun notebook è intercalata nel codice dei notebook stessi.

<!-- Below is the meat - the how to (but without links or details) -->

### Generare dati sintetici {#generate-synthetic-data}

Questo blocco appunti fornisce il codice per generare set di dati di profili sintetici ed eventi di esperienza nella tua piattaforma che verranno utilizzati per illustrare il flusso di lavoro CMLE.

### EDA e funzionalità con Query Service {#eda-and-featurization-with-query-service}

Questo blocco appunti include esempi di analisi esplorativa sui set di dati di Platform utilizzando query interattive tramite Platform Query Service. Seguono esempi di query di feature per creare un set di dati di addestramento per il modello di propensione di esempio.

### Esporta dati di formazione {#export-training-data}

Questo blocco appunti illustra l’esportazione del set di dati di formazione nell’archiviazione cloud che può essere letto dagli strumenti di apprendimento automatico.

### Addestra un modello di propensione {#train-a-propensity-model}

Questo notebook illustra come addestrare un modello di propensione. Considera l’ambiente ML di Databrick come ambiente ML, ma viene scritto in modo generico (ovvero senza un uso intensivo di funzioni/API specifiche di Databrick) in modo che possa essere adattato ad altre piattaforme.

### Punteggio del modello tendenza

Questo notebook illustra il punteggio del modello di propensione addestrato per produrre un set di dati di punteggi di propensione per ogni profilo cliente di Platform.

### Acquisire punteggi in AEP

Questo breve blocco appunti illustra come acquisire il set di dati dei punteggi di tendenza per arricchire i profili cliente in AEP.

### Creare e attivare tipi di pubblico dal codice

Questo blocco appunti illustra come l’utente può creare tipi di pubblico dai punteggi e attivarli tramite le app Platform dal proprio codice di blocco appunti.
