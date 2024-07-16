---
keywords: Experience Platform;preparazione dati;api preparazione dati;risoluzione dei problemi;API
title: Panoramica API della preparazione dati
description: L’API della preparazione dati consente di creare in modo programmatico set di mappatura e funzioni, per trasformare i dati tra schemi di origine e di destinazione.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guida API del servizio di mappatura

La preparazione dati consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM). La preparazione dati viene visualizzata come un passaggio &quot;Mappa&quot; nei processi di acquisizione dati, incluso il flusso di lavoro di acquisizione CSV.

L’API del servizio di mappatura, nota anche come API della preparazione dati, include più endpoint descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

## Funzioni

Le funzioni di mappatura consentono di trasformare i dati tra gli schemi di origine e di destinazione. È possibile utilizzare l&#39;endpoint `/languages/el` per convalidare le espressioni e ottenere un elenco di tutte le funzioni e le operazioni del set di mappatura disponibili.

Per informazioni dettagliate su come utilizzare le funzioni di set di mappatura, leggere la [guida dell&#39;endpoint delle funzioni](./functions.md).

## Set di mappatura

I set di mappatura possono essere utilizzati per definire il modo in cui i dati in uno schema di origine vengono mappati a quelli di uno schema di destinazione. È possibile utilizzare l&#39;endpoint `/mappingSets` nell&#39;API di preparazione dati per recuperare, creare, aggiornare e convalidare a livello di programmazione i set di mappatura.

Per informazioni dettagliate su come utilizzare i set di mappatura, leggere la [guida dell&#39;endpoint del set di mappatura](./mapping-set.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API del servizio di mappatura, leggi la [guida introduttiva](./getting-started.md), quindi seleziona una delle guide dell&#39;endpoint per scoprire come utilizzare gli endpoint specifici.
