---
keywords: ', Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilita profilo;Abilita profilo'
title: Aggiungi dati a profilo cliente in tempo reale
topic: tutorial
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Aggiungi dati a [!DNL Real-time Customer Profile]

Questa esercitazione illustra i passaggi necessari per aggiungere dati a [!DNL Real-time Customer Profile].

## Abilita uno schema per [!DNL Real-time Customer Profile]

I dati che vengono assimilati in [!DNL Experience Platform] per l&#39;utilizzo da parte di [!DNL Real-time Customer Profile] devono essere conformi a uno schema [!DNL Experience Data Model] (XDM) abilitato per [!DNL Profile]. Affinché uno schema sia abilitato per il profilo, deve implementare la classe [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

È possibile abilitare uno schema da utilizzare in [!DNL Real-time Customer Profile] utilizzando l&#39;API [!DNL Schema Registry] o l&#39;interfaccia utente [!DNL Schema Editor]. Per iniziare, seguire le esercitazioni per [creare uno schema utilizzando le API](../../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente dell&#39;Editor schema](../../xdm/tutorials/create-schema-ui.md).

## Aggiunta di dati tramite l&#39;assimilazione batch

Tutti i dati caricati in [!DNL Platform] utilizzando l&#39;assimilazione batch vengono caricati in singoli set di dati. Prima che questi dati possano essere utilizzati da [!DNL Real-time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, vedete l&#39;esercitazione su [configurazione di un set di dati per Profile and Identity Service](dataset-configuration.md).

Una volta configurato il set di dati, è possibile iniziare a assimilarvi i dati. Per informazioni dettagliate sul caricamento di file in diversi formati, consultate la guida per sviluppatori [caricamento batch](../../ingestion/batch-ingestion/api-overview.md).

## Aggiunta di dati tramite caricamento in streaming

Tutti i dati acquisiti dal flusso che sono conformi a uno schema XDM abilitato per [!DNL Profile] aggiungeranno o sovrascriveranno automaticamente il record appropriato in [!DNL Real-time Customer Profile]. Se nel record vengono fornite più identità, o vengono utilizzati dati di serie temporali, tali identità verranno mappate nel grafico dell&#39;identità senza ulteriori configurazioni. Per ulteriori informazioni, vedere la [guida per lo sviluppo dell&#39;assimilazione in streaming](../../ingestion/tutorials/streaming-record-data.md).

## Verificare che il caricamento abbia esito positivo

Quando si caricano i dati su un nuovo dataset per la prima volta, o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzando l&#39;API di accesso [!DNL Real-time Customer Profile] è possibile recuperare i dati batch mentre vengono caricati in un dataset. Se non è possibile recuperare nessuna delle entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, accertati che il formato e gli identificatori dei dati di origine supportino le tue aspettative.

Per istruzioni dettagliate su come accedere alle entità utilizzando l&#39;API [!DNL Real-time Customer Profile], fare riferimento alla guida [endpoint entità](../api/entities.md), nota anche come &quot;[!DNL Profile Access] API&quot;.