---
keywords: Experience Platform;home;argomenti comuni;flussi di dati;flussi di dati;dati;monitoraggio;monitorare flussi di dati;monitorare flussi di dati;monitorare;monitorare flussi di dati;monitorare flussi di dati;monitorare flussi di dati;flusso;servizio di flusso;
solution: Experience Platform
title: Panoramica dei flussi di dati
topic-legacy: overview
description: Questo documento introduce flussi di dati che esprimono il modo in cui vengono utilizzati in Adobe Experience Platform.
exl-id: 8fe08ffa-f095-4e9f-8bab-d060985f0236
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 5%

---

# Panoramica dei dataflows

In Adobe Experience Platform, i dati vengono acquisiti da un’ampia varietà di sorgenti, analizzati all’interno di Experience Platform, e attivati in un’ampia varietà di destinazioni. Platform facilita il processo di tracciamento di questo flusso di dati potenzialmente non lineare grazie alla trasparenza dei flussi di dati.

## Utilizzo dei flussi di dati

I flussi di dati sono una rappresentazione dei processi di dati che consentono di spostare i dati in Platform. Questi flussi di dati sono configurati tra diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, dove vengono quindi utilizzati dal servizio Identity e dal profilo cliente in tempo reale prima di essere infine attivati nelle destinazioni.

Per ulteriori informazioni sull’utilizzo dei dataflows nei connettori sorgente, consulta la sezione [panoramica di origini](../sources/home.md).

## Preparazione dei dati

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

Per ulteriori informazioni sulla preparazione dei dati dopo l’acquisizione, consulta la sezione [Panoramica sulla preparazione dei dati](../data-prep/home.md).

## Monitoraggio dei flussi di dati

I flussi di dati di monitoraggio possono essere eseguiti utilizzando le API di Platform o l’interfaccia utente di Platform. Per informazioni su come monitorare i flussi di dati utilizzando l’API, leggi la [esercitazione API per il monitoraggio dei dataflows](./api/monitor.md). Per informazioni su come monitorare i flussi di dati nell’interfaccia utente di Platform, leggi le esercitazioni su [monitoraggio dei flussi di dati per le origini](./ui/monitor-sources.md) e [monitoraggio dei flussi di dati per le destinazioni](./ui/monitor-destinations.md).
