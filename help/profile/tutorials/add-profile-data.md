---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilitare profilo;abilitare profilo;abilitare profilo
title: Aggiungere dati al profilo cliente in tempo reale
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per aggiungere dati a Real-Time Customer Profile.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Aggiungi dati a [!DNL Real-Time Customer Profile]

Questo tutorial illustra i passaggi necessari per aggiungere dati a [!DNL Real-Time Customer Profile].

## Abilita uno schema per [!DNL Real-Time Customer Profile]

I dati acquisiti in [!DNL Experience Platform] per l&#39;utilizzo da parte di [!DNL Real-Time Customer Profile] devono essere conformi a uno schema [!DNL Experience Data Model] (XDM) abilitato per [!DNL Profile]. Per abilitare uno schema per il profilo, è necessario implementare la classe [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

È possibile abilitare uno schema da utilizzare in [!DNL Real-Time Customer Profile] utilizzando l&#39;API [!DNL Schema Registry] o l&#39;interfaccia utente [!DNL Schema Editor]. Per iniziare, segui i tutorial per [creare uno schema utilizzando le API](../../xdm/tutorials/create-schema-api.md) o [creare uno schema utilizzando l&#39;interfaccia utente dell&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md).

## Aggiungere dati tramite l’acquisizione batch

Tutti i dati caricati in [!DNL Platform] tramite l&#39;acquisizione batch vengono caricati in singoli set di dati. Prima che i dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, consulta l&#39;esercitazione su [configurazione di un set di dati per il profilo e il servizio Identity](dataset-configuration.md).

Una volta configurato il set di dati, puoi iniziare a acquisirvi i dati. Consulta la [guida per gli sviluppatori per l’acquisizione batch](../../ingestion/batch-ingestion/api-overview.md) per i passaggi dettagliati su come caricare i file in formati diversi.

## Aggiungere dati tramite acquisizione in streaming

Qualsiasi dato acquisito dal flusso conforme a uno schema XDM abilitato per [!DNL Profile] aggiungerà o sovrascriverà automaticamente il record appropriato in [!DNL Real-Time Customer Profile]. Se nel record viene fornita più di un’identità o vengono utilizzati dati di serie temporali, queste identità verranno mappate nel grafico delle identità senza ulteriore configurazione. Per ulteriori informazioni, consulta la [guida per gli sviluppatori di Streaming Ingestion](../../ingestion/tutorials/streaming-record-data.md).

## Conferma che il caricamento sia riuscito

Quando si caricano dati in un nuovo set di dati per la prima volta, o come parte di un processo che coinvolge una nuova ETL o sorgente di dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzando l&#39;API di accesso [!DNL Real-Time Customer Profile], è possibile recuperare i dati batch durante il caricamento in un set di dati. Se non riesci a recuperare le entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le aspettative.

Per istruzioni dettagliate su come accedere alle entità utilizzando l&#39;API [!DNL Real-Time Customer Profile], fare riferimento alla [guida dell&#39;endpoint entità](../api/entities.md), nota anche come &quot;[!DNL Profile Access] API&quot;.

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l&#39;esercitazione per [abilitare un set di dati per Profilo e upsert](../../catalog/datasets/enable-upsert.md).
