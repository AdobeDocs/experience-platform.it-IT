---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sui set di dati
topic: datasets
translation-type: tm+mt
source-git-commit: dcdd94a3a13a13b4104e57b74ecf613bc316b0af
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 2%

---


# Panoramica sui set di dati

Tutti i dati che sono stati immessi con successo in Adobe Experience Platform vengono memorizzati nel Data Lake come set di dati. Un dataset è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati archiviati.

Questo documento fornisce una panoramica di alto livello dei set di dati in Experience Platform.

## Creazione di set di dati e tracciamento dei metadati

Catalog Service è il sistema di record per la posizione dei dati e la linea di collegamenti all’interno di Experience Platform e viene utilizzato per creare e gestire i set di dati. Catalog tiene traccia dei metadati per ogni dataset, che include un riferimento allo schema Experience Data Model (XDM) a cui il set di dati è conforme (illustrato nella sezione successiva) e il numero di record immessi nel set di dati.

Per ulteriori informazioni, consultate la panoramica [del servizio](../home.md) catalogo.

## Applicazione di vincoli ai dati del dataset

Experience Data Model (XDM) è il framework standardizzato tramite il quale Platform organizza i dati sull&#39;esperienza cliente. Tutti i dati acquisiti in Platform devono essere conformi a uno schema XDM predefinito prima che possa essere persistente nel Data Lake come dataset.

Tutti i set di dati contengono un riferimento allo schema XDM che vincola il formato e la struttura dei dati che possono memorizzare. Se si tenta di caricare dati in un dataset non conforme allo schema XDM del dataset, l&#39;assimilazione non riuscirà.

Per ulteriori informazioni su XDM, consultate la panoramica [di sistema](../../xdm/home.md)XDM.

## Inserimento di dati nei set di dati

L&#39;inserimento dei dati in Adobe Experience Platform rappresenta i diversi metodi mediante i quali la piattaforma acquisisce i dati da varie origini. Indipendentemente dal metodo di assimilazione, tutti i dati acquisiti con successo vengono convertiti in file batch. I batch sono unità di dati costituite da uno o più file da acquisire come una singola unità. Questi file batch vengono quindi aggiunti ai dataset dedicati e memorizzati all&#39;interno del Data Lake.

Per ulteriori informazioni, consulta la panoramica [sull’inserimento dei](../../ingestion/home.md) dati.

## Applicazione di etichette di utilizzo ai set di dati

Adobe Experience Platform Data Governance consente di gestire i dati dei clienti al fine di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Utilizzando l&#39;etichetta e l&#39;applicazione dell&#39;uso dei dati (DULE) come framework di base, la governance dei dati consente di applicare etichette di utilizzo per classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Le etichette di utilizzo dei dati possono essere applicate a set di dati interi o a singoli campi di set di dati. Le etichette aggiunte a livello di dataset sono ereditate da tutti i campi all&#39;interno di tale dataset.

Per ulteriori informazioni sul servizio, consulta la panoramica [sulla governance dei](../../data-governance/home.md) dati. Per i passaggi su come utilizzare le etichette di utilizzo in [!DNL Platform], consulta le guide seguenti:

* [Gestire le etichette nell’interfaccia](../../data-governance/labels/user-guide.md)
* [Gestire le etichette nell&#39;API](../../data-governance/labels/api.md)

## Set di dati nei servizi della piattaforma a valle

Una volta utilizzati i set di dati per memorizzare i dati acquisiti, tali set di dati vengono utilizzati dai servizi della piattaforma a valle per aggiornare i profili dei clienti, ottenere informazioni approfondite attraverso l&#39;apprendimento automatico e altro ancora.

Di seguito è riportato un elenco di servizi a valle che utilizzano set di dati per varie operazioni. Per ulteriori informazioni, consulta la documentazione relativa a ciascun servizio.

* [API](../../data-access/home.md)di accesso ai dati: Consente di accedere e scaricare il contenuto dei file memorizzati nei set di dati.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Collega le identità tra dispositivi e sistemi, collegando i dataset in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [Profilo](../../profile/home.md)cliente in tempo reale: Sfrutta il servizio Identity per creare profili cliente dettagliati dai set di dati in tempo reale. Il cliente in tempo reale estrae i dati dal Data Lake e persiste nei profili dei clienti nel proprio archivio dati separato.
* [Servizio](../../segmentation/home.md)di segmentazione della piattaforma Adobe Experience: Consente di creare segmenti e generare audience dai dati del profilo cliente in tempo reale. Tali tipi di pubblico possono quindi essere esportati nei propri dataset all&#39;interno del Data Lake.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utilizza l&#39;apprendimento automatico e l&#39;intelligenza artificiale per scoprire informazioni approfondite in insiemi di dati di grandi dimensioni.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Consente di utilizzare SQL standard per eseguire query sui dati in Experience Platform, unire qualsiasi set di dati all&#39;interno del Data Lake e acquisire i risultati delle query come nuovo set di dati da utilizzare nei report, in Data Science Workspace o nel profilo cliente in tempo reale.
* [Adobe Experience Platform Decisioning Service](../../decisioning-service/home.md): Utilizza il profilo cliente in tempo reale per determinare la scelta più probabile che un cliente effettuerà da una serie di opzioni, in base ai dati comportamentali che Profile estrae dai set di dati abilitati.

## Passaggi successivi

Leggendo questo documento, sono stati introdotti gli usi principali dei set di dati in Experience Platform, nonché i vari servizi della piattaforma che utilizzano i set di dati. Per ulteriori dettagli sui diversi modi in cui i set di dati vengono utilizzati in Piattaforma, consulta la documentazione del servizio collegata in questa panoramica.

Per informazioni su come interagire con i set di dati nell’interfaccia utente della piattaforma Experience, consulta la guida [utente](user-guide.md)ai set di dati.