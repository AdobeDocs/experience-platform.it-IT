---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Panoramica sui set di dati
topic: datasets
description: Questo documento fornisce una panoramica di alto livello dei set di dati in  Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 2%

---


# Panoramica sui set di dati

Tutti i dati immessi con successo in Adobe Experience Platform vengono memorizzati [!DNL Data Lake] come set di dati. Un dataset è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati archiviati.

Questo documento fornisce una panoramica di alto livello dei set di dati in [!DNL Experience Platform].

## Creazione di set di dati e tracciamento dei metadati

[!DNL Catalog Service] è il sistema di record per la posizione dei dati e la linea di dati all&#39;interno [!DNL Experience Platform]e viene utilizzato per creare e gestire i set di dati. [!DNL Catalog] tiene traccia dei metadati per ogni dataset, che include un riferimento allo schema [!DNL Experience Data Model] (XDM) a cui è conforme il dataset (illustrato nella sezione successiva) e il numero di record immessi nel set di dati.

Per ulteriori informazioni, consultate la panoramica [del servizio](../home.md) catalogo.

## Applicazione di vincoli ai dati del dataset

[!DNL Experience Data Model] (XDM) è il framework standardizzato tramite il quale [!DNL Platform] vengono organizzati i dati sull&#39;esperienza cliente. Tutti i dati acquisiti [!DNL Platform] devono essere conformi a uno schema XDM predefinito prima di poter essere memorizzati in [!DNL Data Lake] un dataset.

Tutti i set di dati contengono un riferimento allo schema XDM che vincola il formato e la struttura dei dati che possono memorizzare. Se si tenta di caricare dati in un dataset non conforme allo schema XDM del dataset, l&#39;assimilazione non riuscirà.

Per ulteriori informazioni su XDM, consultate la panoramica [di sistema](../../xdm/home.md)XDM.

## Inserimento di dati nei set di dati

Adobe Experience Platform Data Ingestion rappresenta i diversi metodi mediante i quali [!DNL Platform] vengono acquisiti i dati da varie origini. Indipendentemente dal metodo di assimilazione, tutti i dati acquisiti con successo vengono convertiti in file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Questi file batch vengono quindi aggiunti ai set di dati dedicati e memorizzati all&#39;interno dell&#39; [!DNL Data Lake].

Per ulteriori informazioni, consulta la panoramica [sull’inserimento dei](../../ingestion/home.md) dati.

## Applicazione di etichette di utilizzo ai set di dati

Adobe Experience Platform [!DNL Data Governance] consente di gestire i dati dei clienti al fine di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. L’utilizzo dell’etichetta e dell’applicazione dell’uso dei dati (DULE) come framework di base [!DNL Data Governance] consente di applicare etichette di utilizzo per classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Le etichette di utilizzo dei dati possono essere applicate a set di dati interi o a singoli campi di set di dati. Le etichette aggiunte a livello di dataset sono ereditate da tutti i campi all&#39;interno di tale dataset.

Per ulteriori informazioni sul servizio, consulta la panoramica [sulla governance dei](../../data-governance/home.md) dati. Per i passaggi su come utilizzare le etichette di utilizzo in [!DNL Platform], consulta le guide seguenti:

* [Gestire le etichette nell’interfaccia](../../data-governance/labels/user-guide.md)
* [Gestire le etichette dei set di dati nell&#39;API](../../data-governance/labels/dataset-api.md)

## Set di dati nei [!DNL Platform] servizi a valle

Una volta utilizzati i set di dati per memorizzare i dati acquisiti, tali set di dati vengono utilizzati dai [!DNL Platform] servizi a valle per aggiornare i profili dei clienti, acquisire informazioni attraverso l&#39;apprendimento automatico e altro ancora.

Di seguito è riportato un elenco di servizi a valle che utilizzano set di dati per varie operazioni. Per ulteriori informazioni, consulta la documentazione relativa a ciascun servizio.

* [!DNL Data Access API](../../data-access/home.md): Consente di accedere e scaricare il contenuto dei file memorizzati nei set di dati.
* [Servizio](../../identity-service/home.md)identità Adobe Experience Platform: Collega le identità tra dispositivi e sistemi, collegando i dataset in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [!DNL Real-time Customer Profile](../../profile/home.md): Consente [!DNL Identity Service] di creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] estrae i dati dai profili cliente [!DNL Data Lake] e persiste nel proprio archivio dati separato.
* [Servizio](../../segmentation/home.md)di segmentazione Adobe Experience Platform: Consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Tali tipi di pubblico possono quindi essere esportati nei rispettivi set di dati all’interno dell’ [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per scoprire informazioni approfondite in insiemi di dati di grandi dimensioni.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Consente di utilizzare l&#39;SQL standard per eseguire query sui dati [!DNL Experience Platform], unire eventuali set di dati all&#39;interno dei risultati delle query [!DNL Data Lake] e acquisire i risultati come nuovo set di dati da utilizzare nei rapporti [!DNL Data Science Workspace], o [!DNL Real-time Customer Profile].
* [Servizio](../../decisioning-service/home.md)di gestione Adobe Experience Platform: Sfrutta [!DNL Real-time Customer Profile] per determinare la scelta più probabile che un cliente effettuerà da un insieme di opzioni, in base ai dati comportamentali che [!DNL Profile] richiamano dai set di dati abilitati.

## Passaggi successivi

Leggendo questo documento, sono stati introdotti gli usi principali dei set di dati in [!DNL Experience Platform]e i vari [!DNL Platform] servizi che utilizzano i set di dati. Per ulteriori dettagli sui diversi modi in cui vengono utilizzati i set di dati, [!DNL Platform]consulta la documentazione del servizio collegata in questa panoramica.

Per i passaggi su come interagire con i set di dati nell&#39; [!DNL Experience Platform] interfaccia utente, consulta la guida [utente relativa ai](user-guide.md)set di dati.