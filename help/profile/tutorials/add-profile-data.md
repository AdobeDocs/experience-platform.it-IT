---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita profilo;abilita profilo
title: Aggiungere dati al profilo cliente in tempo reale
topic-legacy: tutorial
type: Tutorial
description: Questa esercitazione descrive i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Aggiungi dati a [!DNL Real-Time Customer Profile]

Questa esercitazione descrive i passaggi necessari per aggiungere dati a [!DNL Real-Time Customer Profile].

## Abilita uno schema per [!DNL Real-Time Customer Profile]

Dati da acquisire in [!DNL Experience Platform] per uso da parte di [!DNL Real-Time Customer Profile] devono essere conformi a [!DNL Experience Data Model] Schema (XDM) abilitato per [!DNL Profile]. Affinché uno schema sia abilitato per Profilo, è necessario che implementi [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent] classe.

È possibile abilitare uno schema da utilizzare in [!DNL Real-Time Customer Profile] utilizzando [!DNL Schema Registry] o [!DNL Schema Editor] interfaccia utente. Per iniziare, segui i tutorial per [creazione di uno schema tramite API](../../xdm/tutorials/create-schema-api.md) o [creazione di uno schema tramite l’interfaccia utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).

## Aggiungere dati utilizzando l’acquisizione batch

Tutti i dati caricati in [!DNL Platform] l’utilizzo dell’acquisizione batch viene caricato su singoli set di dati. Prima che questi dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, consulta l’esercitazione su [configurazione di un set di dati per il servizio Profilo e identità](dataset-configuration.md).

Una volta configurato il set di dati, puoi iniziare a assimilarvi i dati. Consulta la sezione [guida per gli sviluppatori di batch ingestion](../../ingestion/batch-ingestion/api-overview.md) per passaggi dettagliati su come caricare i file in diversi formati.

## Aggiungere dati tramite l’acquisizione in streaming

Qualsiasi dato acquisito dal flusso conforme a un [!DNL Profile]Lo schema XDM abilitato aggiunge o sovrascrive automaticamente il record appropriato in [!DNL Real-Time Customer Profile]. Se nel record vengono fornite più identità o vengono utilizzati dati di serie temporali, tali identità verranno mappate nel grafico identità senza configurazioni aggiuntive. Consulta la sezione [guida per sviluppatori di streaming ingestion](../../ingestion/tutorials/streaming-record-data.md) per saperne di più.

## Conferma l’esito positivo del caricamento

Quando carichi i dati in un nuovo set di dati per la prima volta o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, è consigliabile controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzo della [!DNL Real-Time Customer Profile] Access API (API di accesso), è possibile recuperare dati batch durante il caricamento in un set di dati. Se non riesci a recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le tue aspettative.

Per istruzioni dettagliate su come accedere alle entità utilizzando il [!DNL Real-Time Customer Profile] API, fai riferimento al [guida all’endpoint entità](../api/entities.md), noto anche come &quot;[!DNL Profile Access] API&quot;.

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questo può essere fatto tramite l’acquisizione batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per profilo e aggiornamento](../../catalog/datasets/enable-upsert.md).
