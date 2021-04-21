---
keywords: Experience Platform;preparazione dati;api preparazione dati;risoluzione dei problemi;API
title: Panoramica API di preparazione dei dati
topic-legacy: guide
description: L’API di preparazione dei dati consente di creare a livello di programmazione set e funzioni di mappatura che consentono di trasformare i dati tra schemi di origine e di destinazione.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guida all’API del servizio di mappatura

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dei dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dei dati, incluso il flusso di lavoro di acquisizione CSV.

L’API del servizio di mappatura, nota anche come API di preparazione dati, include più endpoint descritti di seguito. Per informazioni dettagliate, visita le singole guide dell&#39;endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

## Funzioni

Le funzioni del set di mappature consentono di trasformare i dati tra schemi di origine e di destinazione. Puoi utilizzare l’endpoint `/languages/el` per convalidare le espressioni e ottenere un elenco di tutte le funzioni e le operazioni disponibili per il set di mappature.

Per informazioni dettagliate su come utilizzare le funzioni del set di mappatura, leggere la [guida endpoint funzioni](./functions.md).

## Set di mappature

I set di mapping possono essere utilizzati per definire il modo in cui i dati di uno schema di origine vengono mappati su quello di uno schema di destinazione. Puoi utilizzare l’endpoint `/mappingSets` nell’API di preparazione dati per recuperare, creare, aggiornare e convalidare a livello di programmazione i set di mappatura.

Per informazioni dettagliate su come utilizzare i set di mappatura, leggere la [guida dei punti finali dei set di mappatura](./mapping-set.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API del servizio di mappatura, leggi la [guida introduttiva](./getting-started.md) , quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare gli endpoint specifici.
