---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Aggiungere dati al profilo cliente in tempo reale
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Aggiungere dati al profilo cliente in tempo reale

Questa esercitazione illustra i passaggi necessari per aggiungere dati al profilo cliente in tempo reale.

## Abilita uno schema per il profilo cliente in tempo reale

I dati che vengono assimilati  Experience Platform per l&#39;utilizzo da parte del profilo cliente in tempo reale devono essere conformi a uno schema XDM (Experience Data Model) abilitato per il profilo. Affinché uno schema sia abilitato per il profilo, deve implementare la classe XDM Singolo profilo o XDM ExperienceEvent.

È possibile abilitare uno schema da utilizzare in Real-time Customer Profile utilizzando l&#39;API del Registro di sistema dello schema o l&#39;interfaccia utente dell&#39;Editor di schema. Per iniziare, seguire le esercitazioni per [creare uno schema utilizzando le API](../../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente](../../xdm/tutorials/create-schema-ui.md)dell&#39;Editor di schema.

## Aggiunta di dati tramite l&#39;assimilazione batch

Tutti i dati caricati in Platform utilizzando l&#39;assimilazione batch vengono caricati in singoli set di dati. Prima che questi dati possano essere utilizzati dal profilo cliente in tempo reale, il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, vedete l&#39;esercitazione sulla [configurazione di un dataset per il servizio](dataset-configuration.md)Profilo e identità.

Una volta configurato il set di dati, è possibile iniziare a assimilarvi i dati. Consultate la guida [per gli sviluppatori per l’assimilazione](../../ingestion/batch-ingestion/api-overview.md) batch per i passaggi dettagliati su come caricare i file in diversi formati.

## Aggiunta di dati tramite caricamento in streaming

Tutti i dati acquisiti dal flusso conformi a uno schema XDM abilitato per il profilo, aggiungeranno o sovrascriveranno automaticamente il record appropriato nel profilo cliente in tempo reale. Se nel record vengono fornite più identità, o vengono utilizzati dati di serie temporali, tali identità verranno mappate nel grafico dell&#39;identità senza ulteriori configurazioni. Per ulteriori informazioni, consulta la guida [per gli sviluppatori per l’assimilazione in](../../ingestion/tutorials/streaming-record-data.md) streaming.

## Verificare che il caricamento abbia esito positivo

Quando si caricano i dati su un nuovo dataset per la prima volta, o come parte di un processo che coinvolge una nuova ETL o una nuova origine dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzando l&#39;API Real-time Customer Profile Access, potete recuperare i dati batch mentre vengono caricati in un dataset. Se non è possibile recuperare le entità previste, il set di dati potrebbe non essere abilitato per il profilo. Dopo aver confermato che il set di dati è stato abilitato, accertati che il formato e gli identificatori dei dati di origine supportino le tue aspettative.

Per istruzioni dettagliate su come accedere alle entità tramite l&#39;API Profilo cliente in tempo reale, consultate la guida [all&#39;endpoint](../api/entities.md)entità, nota anche come &quot;API di accesso profilo&quot;.