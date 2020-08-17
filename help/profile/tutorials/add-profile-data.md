---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable profile;Enable profile
solution: Adobe Experience Platform
title: Aggiungere dati al profilo cliente in tempo reale
topic: tutorial
description: Questa esercitazione illustra i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Aggiungi dati a [!DNL Real-time Customer Profile]

Questa esercitazione descrive i passaggi necessari per aggiungere dati a [!DNL Real-time Customer Profile].

## Abilita uno schema per [!DNL Real-time Customer Profile]

I dati che vengono assimilati [!DNL Experience Platform] per l&#39;utilizzo da [!DNL Real-time Customer Profile] parte devono essere conformi a uno schema [!DNL Experience Data Model] (XDM) abilitato per [!DNL Profile]. Affinché uno schema sia abilitato per il profilo, deve implementare la [!DNL XDM Individual Profile] classe o [!DNL XDM ExperienceEvent] .

È possibile abilitare uno schema da utilizzare [!DNL Real-time Customer Profile] utilizzando l&#39; [!DNL Schema Registry] API o l&#39;interfaccia [!DNL Schema Editor] utente. Per iniziare, seguire le esercitazioni per [creare uno schema utilizzando le API](../../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente](../../xdm/tutorials/create-schema-ui.md)dell&#39;Editor di schema.

## Aggiunta di dati tramite l&#39;assimilazione batch

Tutti i dati caricati per [!DNL Platform] l’assimilazione in batch vengono caricati in singoli set di dati. Prima che questi dati possano essere utilizzati da [!DNL Real-time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, vedete l&#39;esercitazione sulla [configurazione di un dataset per il servizio](dataset-configuration.md)Profilo e identità.

Una volta configurato il set di dati, è possibile iniziare a assimilarvi i dati. Consultate la guida [per gli sviluppatori per l’assimilazione](../../ingestion/batch-ingestion/api-overview.md) batch per i passaggi dettagliati su come caricare i file in diversi formati.

## Aggiunta di dati tramite caricamento in streaming

Tutti i dati acquisiti dal flusso conformi a uno schema XDM [!DNL Profile]abilitato aggiungeranno o sovrascriveranno automaticamente il record appropriato in [!DNL Real-time Customer Profile]. Se nel record vengono fornite più identità, o vengono utilizzati dati di serie temporali, tali identità verranno mappate nel grafico dell&#39;identità senza ulteriori configurazioni. Per ulteriori informazioni, consulta la guida [per gli sviluppatori per l’assimilazione in](../../ingestion/tutorials/streaming-record-data.md) streaming.

## Verificare che il caricamento abbia esito positivo

Quando si caricano i dati su un nuovo dataset per la prima volta, o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzando l&#39;API [!DNL Real-time Customer Profile] Access, è possibile recuperare i dati batch mentre vengono caricati in un dataset. Se non è possibile recuperare le entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, accertati che il formato e gli identificatori dei dati di origine supportino le tue aspettative.

Per istruzioni dettagliate su come accedere alle entità tramite l&#39; [!DNL Real-time Customer Profile] API, consultate la guida [all&#39;endpoint](../api/entities.md)entità, nota anche come &quot;[!DNL Profile Access] API&quot;.