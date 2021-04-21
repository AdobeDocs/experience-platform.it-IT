---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare csv su xdm;guida interfaccia utente;mappatura;mappatura;preparazione dati;preparazione dati;preparazione dei dati;
solution: Experience Platform
title: Panoramica sulla preparazione dei dati
topic-legacy: overview
description: Questo documento introduce Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Panoramica sulla preparazione dei dati

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dei dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dei dati, incluso il flusso di lavoro di acquisizione CSV. I data engineer possono utilizzare Data Prep per eseguire le seguenti manipolazioni dei dati durante l’acquisizione:

- Definire semplici mappature pass-through per assegnare gli attributi di input agli attributi XDM
- Creazione di campi calcolati per eseguire calcoli in riga che possono essere assegnati agli attributi XDM
- Trasforma i dati applicando funzioni di manipolazione di stringa, numeriche o date
- Costruire gerarchie XDM utilizzando funzioni gerarchiche
- Visualizza in anteprima i dati durante la manipolazione all’interno di Data Prep

Data Prep applica anche diverse convalide di dati intrinseci per garantire che l’integrità dei dati venga mantenuta durante l’acquisizione. Laddove possibile, Data Prep mappa automaticamente gli schemi di dati in arrivo su XDM. I data engineer possono modificare, correggere ed eliminare le mappature suggerite e sostituirle con le mappature appropriate.

## Mappatura

Una mappatura è un&#39;associazione di un attributo di input o di un campo calcolato a un attributo XDM. Un singolo attributo può essere mappato su più attributi XDM creando mappature individuali.

Per ulteriori informazioni sulle diverse funzioni di mappatura, leggere la [guida alle funzioni di mappatura](./functions.md).

## Set di mappature

Un set di mappature che trasformano uno schema in un altro è noto collettivamente come set di mappature. Viene creato un singolo set di mappatura come parte di ciascun flusso di dati. Un set di mappatura è parte integrante dei flussi di dati e viene creato, modificato e monitorato come parte dei flussi di dati.

## Gestione del formato dati

Data Prep può gestire in modo affidabile diversi formati di dati acquisiti in Platform. Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, leggere la [panoramica sulla gestione del formato dati](./data-handling.md).

## Passaggi successivi

Questo documento illustra le nozioni di base sulla preparazione dei dati in Adobe Experience Platform. Per ulteriori informazioni sulle diverse funzioni di mappatura, leggere la [guida alle funzioni di mappatura](./functions.md). Per ulteriori informazioni su come Data Prep gestisce diversi tipi di dati, consulta la [guida alla gestione del formato dei dati](./data-handling.md#dates). Per informazioni su come utilizzare l&#39;API di preparazione dati, leggi la [Guida per gli sviluppatori di preparazione dati](api/overview.md).
