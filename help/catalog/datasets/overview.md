---
keywords: Experience Platform;home;argomenti popolari;posizione dati;posizione dati;gestione dati;gestione dati;linea;linea;linea;tipo di dati;tipi di dati;tipi di dati;tipo di dati
solution: Experience Platform
title: Panoramica dei set di dati
topic-legacy: datasets
description: Questo documento fornisce una panoramica di alto livello dei set di dati in Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 02002c9530074b8b05664ff9eab5bc2fe4b7d5d4
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 8%

---

# Panoramica dei set di dati

Tutti i dati che vengono correttamente acquisiti in Adobe Experience Platform vengono memorizzati nella variabile [!DNL Data Lake] come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

Questo documento fornisce una panoramica di alto livello dei set di dati in [!DNL Experience Platform].

## Creazione di set di dati e metadati di tracciamento

[!DNL Catalog Service] è il sistema di registrazione per la posizione dei dati e la derivazione all&#39;interno di [!DNL Experience Platform], e viene utilizzato per creare e gestire i set di dati. [!DNL Catalog] tiene traccia dei metadati per ogni set di dati, che include un riferimento al [!DNL Experience Data Model] (XDM) schema a cui è conforme il set di dati (illustrato nella sezione successiva) e numero di record acquisiti in tale set di dati.

Consulta la sezione [Panoramica del servizio catalogo](../home.md) per ulteriori informazioni.

## Applicazione dei vincoli ai dati dei set di dati

[!DNL Experience Data Model] (XDM) è il quadro standardizzato tramite il quale [!DNL Platform] organizza i dati sulla customer experience. Tutti i dati acquisiti in [!DNL Platform] deve essere conforme a uno schema XDM predefinito prima di poter essere mantenuto nel [!DNL Data Lake] come set di dati.

Tutti i set di dati contengono un riferimento allo schema XDM che vincola il formato e la struttura dei dati che possono memorizzare. Il tentativo di caricare dati in un set di dati non conforme allo schema XDM del set di dati causerà errori di inserimento.

Per ulteriori informazioni su XDM, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Acquisizione di dati nei set di dati

L’acquisizione dei dati Adobe Experience Platform rappresenta i diversi metodi con cui [!DNL Platform] acquisisce dati da varie sorgenti. Indipendentemente dal metodo di acquisizione, tutti i dati correttamente acquisiti vengono convertiti in file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Questi file batch vengono quindi aggiunti ai set di dati dedicati e mantenuti all&#39;interno di [!DNL Data Lake].

Consulta la sezione [Panoramica sull’acquisizione dei dati](../../ingestion/home.md) per ulteriori informazioni.

## Applicazione delle etichette di utilizzo ai set di dati

La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti al fine di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Il framework per la governance dei dati ti consente di applicare etichette di utilizzo per classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Le etichette di utilizzo dei dati possono essere applicate a interi set di dati o a singoli campi di set di dati. Le etichette aggiunte a livello di set di dati vengono ereditate da tutti i campi all’interno di tale set di dati.

Consulta la sezione [Panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni sul servizio. Per i passaggi su come utilizzare le etichette di utilizzo in [!DNL Platform], consulta le seguenti guide:

* [Gestire le etichette nell’interfaccia utente](../../data-governance/labels/user-guide.md)
* [Gestire le etichette dei set di dati nell’API](../../data-governance/labels/dataset-api.md)

## Set di dati a valle [!DNL Platform] servizi

Una volta utilizzati i set di dati per memorizzare i dati acquisiti, questi vengono utilizzati da downstream [!DNL Platform] servizi per aggiornare i profili dei clienti, ottenere informazioni attraverso l’apprendimento automatico e altro ancora.

Di seguito è riportato un elenco di servizi a valle che utilizzano set di dati per varie operazioni. Per ulteriori informazioni, consulta la documentazione relativa a ciascun servizio.

* [[!DNL Data Access API]](../../data-access/home.md): Consente di accedere e scaricare il contenuto dei file memorizzati all’interno dei set di dati.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): Collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Sfruttamento [!DNL Identity Service] per creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] richiama i dati dal [!DNL Data Lake] e persiste i profili dei clienti nel proprio archivio dati separato.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): Consente di creare segmenti e generare tipi di pubblico dai [!DNL Real-time Customer Profile] dati. Questi tipi di pubblico possono quindi essere esportati nei rispettivi set di dati all’interno di [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utilizza l’apprendimento automatico e l’intelligenza artificiale per individuare informazioni in set di dati di grandi dimensioni.
* [Servizio query Adobe Experience Platform](../../query-service/home.md): Consente di utilizzare SQL standard per eseguire query sui dati in [!DNL Experience Platform], unione di qualsiasi set di dati all’interno di [!DNL Data Lake] e la cattura dei risultati delle query come nuovo set di dati da utilizzare nei rapporti, [!DNL Data Science Workspace]oppure [!DNL Real-time Customer Profile].
* [Servizio Destinazioni Adobe Experience Platform](../../destinations/home.md): Permette di [esportare i set di dati](/help/destinations/ui/export-datasets.md) alle tue destinazioni di marketing e-mail o di archiviazione cloud desiderate, per attività di reporting o data science.

## Passaggi successivi

Leggendo questo documento, sei stato introdotto agli usi principali dei set di dati in [!DNL Experience Platform], nonché i vari [!DNL Platform] servizi che utilizzano set di dati. Per ulteriori dettagli sui diversi modi in cui i set di dati vengono utilizzati in [!DNL Platform], consulta la documentazione del servizio collegata in questa panoramica.

Per i passaggi su come interagire con i set di dati all’interno di [!DNL Experience Platform] Interfaccia utente, vedi [guida utente dei set di dati](user-guide.md).
