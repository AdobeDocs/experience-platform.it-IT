---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;abilitare profilo;abilitare profilo;abilitare profilo
title: Aggiungere dati al profilo cliente in tempo reale
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per aggiungere dati a Real-Time Customer Profile.
exl-id: c2df224b-bf3d-4994-aa3a-9e9f4a6a726c
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Aggiungi dati a [!DNL Real-Time Customer Profile]

Questo tutorial illustra i passaggi necessari per aggiungere dati a [!DNL Real-Time Customer Profile].

## Abilita uno schema per [!DNL Real-Time Customer Profile]

Dati acquisiti in [!DNL Experience Platform] per l’utilizzo da [!DNL Real-Time Customer Profile] deve essere conforme a un [!DNL Experience Data Model] Schema (XDM) abilitato per [!DNL Profile]. Per abilitare uno schema per il profilo, è necessario implementare [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent] classe.

È possibile abilitare uno schema per l’utilizzo in [!DNL Real-Time Customer Profile] utilizzando [!DNL Schema Registry] API o [!DNL Schema Editor] dell&#39;utente. Per iniziare, segui i tutorial per [creazione di uno schema tramite API](../../xdm/tutorials/create-schema-api.md) o [creazione di uno schema tramite l’interfaccia utente dell’Editor di schema](../../xdm/tutorials/create-schema-ui.md).

## Aggiungere dati tramite l’acquisizione batch

Tutti i dati caricati in [!DNL Platform] l’utilizzo dell’acquisizione batch viene caricato nei singoli set di dati. Prima che questi dati possano essere utilizzati da [!DNL Real-Time Customer Profile], il set di dati in questione deve essere configurato in modo specifico. Per istruzioni complete, consulta l’esercitazione su [configurazione di un set di dati per Profilo e Identity Service](dataset-configuration.md).

Una volta configurato il set di dati, puoi iniziare a acquisirvi i dati. Consulta la [guida per gli sviluppatori sull’acquisizione batch](../../ingestion/batch-ingestion/api-overview.md) per i passaggi dettagliati su come caricare i file in formati diversi.

## Aggiungere dati tramite acquisizione in streaming

Qualsiasi dato acquisito in streaming che è conforme a un [!DNL Profile]Lo schema XDM abilitato aggiungerà o sovrascriverà automaticamente il record appropriato in [!DNL Real-Time Customer Profile]. Se nel record viene fornita più di un’identità o vengono utilizzati dati di serie temporali, queste identità verranno mappate nel grafico delle identità senza ulteriore configurazione. Consulta la [guida per gli sviluppatori sull’acquisizione in streaming](../../ingestion/tutorials/streaming-record-data.md) per ulteriori informazioni.

## Conferma che il caricamento sia riuscito

Quando si caricano dati in un nuovo set di dati per la prima volta, o come parte di un processo che coinvolge una nuova ETL o sorgente di dati, si consiglia di controllare attentamente i dati per assicurarsi che siano stati caricati correttamente.

Utilizzo di [!DNL Real-Time Customer Profile] Access API (API di Access), puoi recuperare i dati batch non appena vengono caricati in un set di dati. Se non riesci a recuperare le entità previste, il set di dati potrebbe non essere abilitato per [!DNL Profile]. Dopo aver confermato che il set di dati è stato abilitato, assicurati che il formato e gli identificatori dei dati di origine supportino le aspettative.

Per istruzioni dettagliate su come accedere alle entità utilizzando [!DNL Real-Time Customer Profile] API, fare riferimento al [guida dell’endpoint &quot;entities&quot;](../api/entities.md), noto anche come &quot;[!DNL Profile Access] API&quot;.

## Aggiorna dati archivio profili

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questa operazione può essere eseguita tramite l’acquisizione in batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per Profilo e upsert](../../catalog/datasets/enable-upsert.md).
