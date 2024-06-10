---
solution: Experience Platform
title: Glossario dei Adobi Experience Platform Destination SDK
description: Comprendi la terminologia importante quando crei una destinazione utilizzando Experienci Platform Destination SDK.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---


# Glossario dei Adobi Experience Platform Destination SDK

Per le definizioni dei termini utilizzati nella Destination SDK, consultare questo glossario. Per altri termini di Adobe Experience Platform, consulta [Glossario di Experience Platform](/help/landing/glossary.md).

## A

**Criterio di aggregazione**: quando configuri il modo in cui i dati devono essere esportati nella destinazione di streaming in tempo reale, puoi definire il modo in cui i dati del profilo vengono aggregati prima di essere inviati alla piattaforma di destinazione. Questo consente di ottimizzare la distribuzione dei dati raggruppando i record di dati in base a criteri specifici, riducendo la frequenza delle chiamate API e migliorando l’efficienza complessiva. È possibile configurare criteri diversi per soddisfare i vari requisiti di destinazione, garantendo che i dati vengano inseriti in un pacchetto e consegnati nel modo più efficace possibile. [Ulteriori informazioni](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configurazione dei metadati del pubblico**: per configurazione di metadati di pubblico si intendono la configurazione strutturata e i parametri definiti in Adobe Experience Platform che consentono la creazione, l’aggiornamento e l’eliminazione programmatici dei segmenti di pubblico in una destinazione specifica. Questa configurazione utilizza modelli di metadati del pubblico per allinearli alle specifiche dell’API di marketing della piattaforma di destinazione. Ulteriori informazioni su [configurazione dei metadati del pubblico](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) e [macro disponibili](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Endpoint di configurazione della destinazione**: endpoint di configurazione di destinazione in Adobe Experience Platform, in particolare `/authoring/destinations` L’endpoint API viene utilizzato per creare, recuperare, aggiornare ed eliminare configurazioni per le destinazioni. Queste configurazioni definiscono il modo in cui i dati da Adobe Experience Platform vengono consegnati a vari sistemi o destinazioni esterni, come piattaforme di marketing, servizi di archiviazione cloud o altri endpoint di elaborazione dati. Ulteriori informazioni su [opzioni di configurazione disponibili](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) e visualizzare [documentazione di riferimento](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Istanza di destinazione**: configurazione specifica di una configurazione di destinazione in Adobe Experience Platform, creata e gestita tramite l’interfaccia utente di Experienci Platform. Include tutti i parametri e le credenziali necessari per la connessione e l’invio di dati alla destinazione. Dopo aver stabilito la connessione alla destinazione, puoi ottenere l’ID istanza di destinazione quando [esplorazione di una connessione con la destinazione](/help/destinations/ui/destination-details-page.md).

![Immagine dell’interfaccia utente per ottenere l’ID dell’istanza di destinazione](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]modello**: A [!DNL Pebble] Questo modello viene utilizzato per trasformare i dati esportati da Adobe Experience Platform nel formato richiesto dalla piattaforma di destinazione. Utilizza il [!DNL Pebble] Template Language, che consente la trasformazione dinamica dei dati tramite funzioni come `filter`, `for`, `if`, e `set`. Adobe Experience Platform include funzioni personalizzate aggiuntive, come `addedSegments` e `removedSegments`. Questi modelli consentono di formattare elementi dati, come marche temporali e appartenenze a un pubblico, per soddisfare le specifiche della destinazione. Ulteriori informazioni [qui](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) e [qui](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Destinazione privata**: integrazioni personalizzate create da singoli clienti Adobe Experience Platform. Questi sono personalizzati per soddisfare specifiche esigenze aziendali e sono accessibili solo all’interno dell’organizzazione del cliente, offrendo flessibilità nelle configurazioni di esportazione dei dati. Le destinazioni private sono disponibili solo per i clienti di Real-Time CDP Ultimate. [Ulteriori informazioni](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Destinazione pubblica**: integrazione disponibile pubblicamente nel catalogo Adobe Experience Platform. Queste destinazioni sono standardizzate, con marchio e semplificano la configurazione dei clienti fornendo parametri preconfigurati. Sono accessibili a tutti i clienti che utilizzano Adobe Experience Platform. [Ulteriori informazioni](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Modello di documentazione self-service**: il modello di documentazione self-service fornisce un formato strutturato che è possibile utilizzare per documentare la destinazione. Include sezioni per una panoramica, casi di utilizzo, prerequisiti, identità supportate, tipi di pubblico, tipi di esportazione e frequenza, nonché passaggi per la connessione alla destinazione, l’attivazione dei tipi di pubblico e la mappatura degli attributi. Utilizza questo modello per garantire una documentazione completa e coerente, che consenta ai clienti di iniziare rapidamente a utilizzare la destinazione e di comprendere i casi di utilizzo forniti. Ulteriori informazioni su [come documentare la destinazione](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [scarica il modello di documentazione self-service più recente](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), e [visualizza il rendering](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Specifiche dei modelli e strategie di modelli**: le specifiche del modello sono configurazioni utilizzate per formattare le richieste HTTP inviate da Adobe Experience Platform a una destinazione. Trasformano i campi degli attributi del profilo dallo schema XDM in un formato supportato dalla piattaforma di destinazione. Utilizzo di un linguaggio per modelli simile a [!DNL Jinja], queste specifiche consentono trasformazioni di dati dinamiche basate su regole specifiche e dati di input. [Ulteriori informazioni](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Test dell’API**: l’API di test consente di convalidare le configurazioni di destinazione prima di inviare una richiesta di pubblicazione. Fornisce strumenti per generare profili di esempio e testare il flusso di dati, garantendo che la configurazione corrisponda ai requisiti della destinazione. L’API supporta sia le destinazioni in streaming che quelle basate su file (batch), offrendo un modo per simulare i dati e risolvere potenziali problemi nel processo di configurazione. Ulteriori informazioni sull’API di test per [streaming](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) e [destinazioni basate su file](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Modello di trasformazione**: un modello di trasformazione personalizza il formato dei dati dallo schema XDM di Adobe al formato previsto della destinazione. [Ulteriori informazioni](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).