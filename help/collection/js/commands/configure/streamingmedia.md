---
title: streamingMedia
description: Configura il Web SDK per raccogliere i dati relativi all’utilizzo dei contenuti multimediali nelle proprietà web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

Il componente `streamingMedia` consente di raccogliere i dati relativi alle sessioni multimediali sul sito Web.

I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a Adobe Experience Platform o Adobe Analytics per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

## Prerequisiti

Per utilizzare il componente `streamingMedia` del Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Assicurati di avere accesso a Adobe Experience Platform o Adobe Analytics.
* È necessario utilizzare Web SDK versione 2.20.0 o successiva. Per informazioni su come installare la versione più recente, consulta la [panoramica sull&#39;installazione di Web SDK](../../install/overview.md).
* Abilitare l&#39;opzione **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nel Web SDK, come illustrato in questa pagina.

Quando si chiama il comando `configure`, aggiungere l&#39;oggetto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Proprietà | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| **`channel`** | Stringa | Sì | Nome del canale in cui si verifica la raccolta di contenuti multimediali in streaming. Esempio: `Video channel`. |
| **`playerName`** | Stringa | Sì | Nome del lettore multimediale. |
| **`appVersion`** | Stringa | No | Versione dell’applicazione lettore multimediale. |
| **`mainPingInterval`** | Intero | No | Frequenza dei ping per il contenuto principale, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `10` e `50` secondi.  Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](../createmediasession.md#automatic). |
| **`adPingInterval`** | Intero | No | Frequenza dei ping per il contenuto dell’annuncio, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `1` e `10` secondi. Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](../createmediasession.md#automatic). |

## Configurazione di contenuti multimediali in streaming tramite l’estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione di Streaming Media](/help/tags/extensions/client/web-sdk/configure/streaming-media.md).
