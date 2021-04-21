---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita profilo;abilita profilo
title: Aggiungere dati al profilo cliente in tempo reale
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Aggiungi dati a [!DNL Real-time Customer Profile]

Questa esercitazione descrive i passaggi necessari per aggiungere dati a [!DNL Real-time Customer Profile].

## Abilita uno schema per [!DNL Real-time Customer Profile]

I dati che vengono acquisiti in [!DNL Experience Platform] per l&#39;utilizzo da [!DNL Real-time Customer Profile] devono essere conformi a uno schema [!DNL Experience Data Model] (XDM) abilitato per [!DNL Profile]. Affinché uno schema sia abilitato per Profilo, deve implementare la classe [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent] .

È possibile abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile] utilizzando l&#39;API [!DNL Schema Registry] o l&#39;interfaccia utente [!DNL Schema Editor]. Per iniziare, segui le esercitazioni per [creare uno schema utilizzando API](../../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente dell&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md).

## Aggiungere dati utilizzando l’acquisizione batch

Tutti i dati caricati in [!DNL Platform] utilizzando l’acquisizione batch vengono caricati in singoli set di dati. Prima che questi dati possano essere utilizzati da [!DNL Real-time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, consulta l’esercitazione su [configurazione di un set di dati per il servizio Profilo e identità](dataset-configuration.md).

Una volta configurato il set di dati, puoi iniziare a assimilarvi i dati. Per informazioni dettagliate su come caricare i file in formati diversi, consulta la [guida per gli sviluppatori di inserimento batch](../../ingestion/batch-ingestion/api-overview.md) .

## Aggiungere dati tramite l’acquisizione in streaming

Tutti i dati acquisiti dal flusso conformi a uno schema XDM abilitato [!DNL Profile] aggiungeranno o sovrascriveranno automaticamente il record appropriato in [!DNL Real-time Customer Profile]. Se nel record vengono fornite più identità o vengono utilizzati dati di serie temporali, tali identità verranno mappate nel grafico identità senza configurazioni aggiuntive. Per ulteriori informazioni, consulta la [guida per sviluppatori per l’acquisizione in streaming](../../ingestion/tutorials/streaming-record-data.md) .

## Conferma l’esito positivo del caricamento

Quando carichi i dati in un nuovo set di dati per la prima volta o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, è consigliabile controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzando l’ API di accesso [!DNL Real-time Customer Profile] è possibile recuperare i dati batch caricati in un set di dati. Se non riesci a recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le tue aspettative.

Per istruzioni dettagliate su come accedere alle entità utilizzando l&#39;API [!DNL Real-time Customer Profile], fai riferimento alla [guida all&#39;endpoint entità](../api/entities.md), nota anche come &quot;[!DNL Profile Access] API&quot;.
