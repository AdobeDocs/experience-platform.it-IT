---
keywords: Experience Platform;home;argomenti popolari;posizione dati;posizione dati;gestione dati;gestione dati;linea;linea;linea;tipo di dati;tipi di dati;tipi di dati;tipo di dati
solution: Experience Platform
title: Panoramica dei set di dati
topic-legacy: datasets
description: Questo documento fornisce una panoramica di alto livello dei set di dati in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%

---

# Panoramica dei set di dati

Tutti i dati correttamente acquisiti in Adobe Experience Platform vengono memorizzati come set di dati all’interno di [!DNL Data Lake]. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

Questo documento fornisce una panoramica di alto livello dei set di dati in [!DNL Experience Platform].

## Creazione di set di dati e metadati di tracciamento

[!DNL Catalog Service] è il sistema di record per la posizione e la derivazione dei dati all’interno di  [!DNL Experience Platform] e viene utilizzato per creare e gestire i set di dati. [!DNL Catalog] tiene traccia dei metadati per ogni set di dati, che include un riferimento allo schema  [!DNL Experience Data Model] (XDM) a cui è conforme il set di dati (spiegato nella sezione successiva) e al numero di record acquisiti in tale set di dati.

Per ulteriori informazioni, consulta la [Panoramica del servizio catalogo](../home.md) .

## Applicazione dei vincoli ai dati dei set di dati

[!DNL Experience Data Model] (XDM) è il framework standardizzato tramite il quale  [!DNL Platform] organizza i dati sulla customer experience. Tutti i dati acquisiti in [!DNL Platform] devono essere conformi a uno schema XDM predefinito prima di poter essere mantenuti in [!DNL Data Lake] come set di dati.

Tutti i set di dati contengono un riferimento allo schema XDM che vincola il formato e la struttura dei dati che possono memorizzare. Il tentativo di caricare dati in un set di dati non conforme allo schema XDM del set di dati causerà errori di inserimento.

Per ulteriori informazioni su XDM, consulta la [Panoramica del sistema XDM](../../xdm/home.md).

## Acquisizione di dati nei set di dati

L’acquisizione dei dati di Adobe Experience Platform rappresenta i diversi metodi con cui [!DNL Platform] acquisisce i dati da varie sorgenti. Indipendentemente dal metodo di acquisizione, tutti i dati correttamente acquisiti vengono convertiti in file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Questi file batch vengono quindi aggiunti ai set di dati dedicati e mantenuti all&#39;interno di [!DNL Data Lake].

Per ulteriori informazioni, consulta la [Panoramica sull’acquisizione dei dati](../../ingestion/home.md) .

## Applicazione delle etichette di utilizzo ai set di dati

Adobe Experience Platform [!DNL Data Governance] ti consente di gestire i dati dei clienti al fine di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Il framework [!DNL Data Governance] ti consente di applicare etichette di utilizzo per classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Le etichette di utilizzo dei dati possono essere applicate a interi set di dati o a singoli campi di set di dati. Le etichette aggiunte a livello di set di dati vengono ereditate da tutti i campi all’interno di tale set di dati.

Per ulteriori informazioni sul servizio, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) . Per i passaggi su come utilizzare le etichette di utilizzo in [!DNL Platform], consulta le seguenti guide:

* [Gestire le etichette nell’interfaccia utente](../../data-governance/labels/user-guide.md)
* [Gestire le etichette dei set di dati nell’API](../../data-governance/labels/dataset-api.md)

## Set di dati nei servizi a valle [!DNL Platform]

Una volta utilizzati i set di dati per memorizzare i dati acquisiti, questi vengono quindi utilizzati dai servizi a valle [!DNL Platform] per aggiornare i profili dei clienti, ottenere informazioni attraverso l’apprendimento automatico e altro ancora.

Di seguito è riportato un elenco di servizi a valle che utilizzano set di dati per varie operazioni. Per ulteriori informazioni, consulta la documentazione relativa a ciascun servizio.

* [[!DNL Data Access API]](../../data-access/home.md): Consente di accedere e scaricare il contenuto dei file memorizzati all’interno dei set di dati.
* [Servizio](../../identity-service/home.md) Adobe Experience Platform Identity: Collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Utilizza  [!DNL Identity Service] per creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] richiama i dati dai profili cliente  [!DNL Data Lake] e persiste nel proprio archivio dati separato.
* [Servizio](../../segmentation/home.md) di segmentazione di Adobe Experience Platform: Ti consente di creare segmenti e generare tipi di pubblico dai  [!DNL Real-time Customer Profile] dati. Questi tipi di pubblico possono quindi essere esportati nei rispettivi set di dati all’interno di [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utilizza l’apprendimento automatico e l’intelligenza artificiale per individuare informazioni in set di dati di grandi dimensioni.
* [Servizio](../../query-service/home.md) query Adobe Experience Platform: Consente di utilizzare SQL standard per eseguire query sui dati in  [!DNL Experience Platform], unire qualsiasi set di dati all’interno di  [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting,  [!DNL Data Science Workspace]o  [!DNL Real-time Customer Profile].

## Passaggi successivi

Leggendo questo documento, sei stato introdotto agli usi principali dei set di dati in [!DNL Experience Platform], nonché ai vari servizi [!DNL Platform] che utilizzano i set di dati. Per ulteriori dettagli sui diversi modi in cui i set di dati vengono utilizzati in [!DNL Platform], consulta la documentazione del servizio collegata in questa panoramica.

Per i passaggi su come interagire con i set di dati all’interno dell’ [!DNL Experience Platform] interfaccia utente, consulta la [guida utente per i set di dati](user-guide.md).
