---
keywords: Experience Platform;home;argomenti popolari;posizione dati;posizione dati;gestione dati;gestione dati;derivazione;tipo di dati;tipi di dati;tipi di dati;tipo di dati;home;popular topic;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Panoramica dei set di dati
description: Questo documento fornisce una panoramica di alto livello dei set di dati in Experience Platform.
user-guide-description: Ottieni una panoramica di alto livello dei set di dati nell’Experience Platform con questa guida. Scopri come crearli, applicare vincoli sui dati e acquisire dati nei set di dati qui.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 6%

---

# Panoramica sui set di dati

Tutti i dati acquisiti correttamente in Adobe Experience Platform vengono mantenuti all&#39;interno di [!DNL Data Lake] come set di dati. Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

Questo documento fornisce una panoramica di alto livello dei set di dati in [!DNL Experience Platform].

## Creazione di set di dati e metadati di tracciamento

[!DNL Catalog Service] è il sistema di registrazione per la posizione e la derivazione dei dati in [!DNL Experience Platform] e viene utilizzato per creare e gestire i set di dati. [!DNL Catalog] tiene traccia dei metadati per ogni set di dati, che include un riferimento allo schema [!DNL Experience Data Model] (XDM) a cui il set di dati è conforme (illustrato nella sezione successiva) e del numero di record acquisiti in tale set di dati.

Per ulteriori informazioni, vedere [Panoramica di Catalog Service](../home.md).

## Applicazione di vincoli ai dati dei set di dati

[!DNL Experience Data Model] (XDM) è il framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente. Tutti i dati acquisiti in [!DNL Platform] devono essere conformi a uno schema XDM predefinito prima di poter essere memorizzati in [!DNL Data Lake] come set di dati.

Tutti i set di dati contengono un riferimento allo schema XDM che limita il formato e la struttura dei dati che possono memorizzare. Il tentativo di caricare dati in un set di dati non conforme allo schema XDM del set di dati causerà un errore di acquisizione.

Per ulteriori informazioni su XDM, consulta la [Panoramica del sistema XDM](../../xdm/home.md).

## Acquisizione di dati nei set di dati

L&#39;acquisizione dati di Adobe Experience Platform rappresenta i diversi metodi con cui [!DNL Platform] acquisisce dati da varie origini. Indipendentemente dal metodo di acquisizione, tutti i dati acquisiti correttamente vengono convertiti in file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Questi file batch vengono quindi aggiunti ai set di dati dedicati e memorizzati in [!DNL Data Lake].

Per ulteriori informazioni, consulta la [Panoramica sull&#39;acquisizione dei dati](../../ingestion/home.md).

## Etichette applicate ai set di dati dagli schemi

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti al fine di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Il framework di governance dei dati consente di applicare le etichette di utilizzo per categorizzare i dati in base ai criteri di utilizzo applicabili a tali dati. Le etichette possono essere applicate a singoli schemi, campi all’interno di tali schemi e interi set di dati individuali. Quando le etichette vengono applicate direttamente a uno schema, vengono propagate a tutti i set di dati esistenti e futuri basati su tale schema.

>[!IMPORTANT]
>
>Le etichette non possono più essere applicate ai campi a livello di set di dati. Questo flusso di lavoro è stato dichiarato obsoleto a favore dell’applicazione di etichette a livello di schema. Eventuali etichette applicate in precedenza a livello di oggetto del set di dati continueranno a essere supportate tramite l’interfaccia utente di Platform fino al 31 maggio 2024. Per garantire che le etichette siano coerenti in tutti gli schemi, tutte le etichette precedentemente associate ai campi a livello di set di dati devono essere migrate a livello di schema da te nel corso dell’anno successivo. Per istruzioni su come eseguire questa operazione, consulta la sezione sulla [migrazione delle etichette applicate in precedenza](../../data-governance/e2e.md#migrate-labels).

Per ulteriori informazioni sul servizio, vedere [Panoramica sulla governance dei dati](../../data-governance/home.md). Per i passaggi su come utilizzare le etichette di utilizzo in [!DNL Platform], consultare le seguenti guide:

* [Gestire le etichette nell’interfaccia utente](../../data-governance/labels/user-guide.md)
* [Gestire le etichette dei set di dati nell’API](../../data-governance/labels/dataset-api.md)

## Set di dati nei servizi [!DNL Platform] a valle

Una volta utilizzati i set di dati per archiviare i dati acquisiti, questi vengono utilizzati dai servizi [!DNL Platform] a valle per aggiornare i profili dei clienti, ottenere informazioni approfondite tramite l&#39;apprendimento automatico e altro ancora.

Di seguito è riportato un elenco di servizi a valle che utilizzano i set di dati per varie operazioni. Per ulteriori informazioni, consulta la documentazione di ciascun servizio.

* [[!DNL Data Access API]](../../data-access/home.md): consente di accedere e scaricare il contenuto dei file memorizzati nei set di dati.
* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): sfrutta [!DNL Identity Service] per creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-Time Customer Profile] estrae dati da [!DNL Data Lake] e mantiene i profili cliente nel proprio archivio dati separato.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): consente di creare segmenti e generare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico possono quindi essere esportati nei propri set di dati in [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per individuare informazioni in set di dati di grandi dimensioni.
* [Servizio query Adobe Experience Platform](../../query-service/home.md): consente di utilizzare SQL standard per eseguire query sui dati in [!DNL Experience Platform], unire qualsiasi set di dati all&#39;interno di [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, [!DNL Data Science Workspace] o [!DNL Real-Time Customer Profile].
* [Servizio destinazioni Adobe Experience Platform](../../destinations/home.md): ti consente di [esportare i set di dati](/help/destinations/ui/export-datasets.md) nell&#39;archiviazione cloud desiderata o nelle destinazioni di e-mail marketing, per attività di reporting o di data science.

## Passaggi successivi

Dopo aver letto questo documento, potrai conoscere gli utilizzi principali dei set di dati in [!DNL Experience Platform] e dei vari servizi [!DNL Platform] che utilizzano i set di dati. Per ulteriori dettagli sui diversi modi in cui i set di dati vengono utilizzati in [!DNL Platform], consulta la documentazione del servizio collegata in questa panoramica.

Per i passaggi su come interagire con i set di dati nell&#39;interfaccia utente [!DNL Experience Platform], consulta la [guida utente per i set di dati](user-guide.md).
