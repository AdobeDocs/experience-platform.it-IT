---
title: streamingMedia
description: Configura l’SDK per web per raccogliere i dati relativi all’utilizzo dei contenuti multimediali nelle proprietà web.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

Il componente `streamingMedia` consente di raccogliere i dati relativi alle sessioni multimediali sul sito Web.

I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a Adobe Experience Platform e/o Adobe Analytics, per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

## Prerequisiti {#prerequisites}

Per utilizzare il componente `streamingMedia` di Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Assicurati di avere accesso a Adobe Experience Platform e/o Adobe Analytics.
* È necessario utilizzare Web SDK versione 2.20.0 o successiva. Per informazioni su come installare la versione più recente, consulta la [panoramica sull&#39;installazione di Web SDK](../../install/overview.md).
* Abilita l&#39;opzione **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nella configurazione dell&#39;SDK Web, come illustrato in questa pagina, tramite l&#39;[estensione tag](#tag-extension) o tramite la [libreria JavaScript](#library).

## Configurare i contenuti multimediali in streaming utilizzando l’estensione tag Web SDK {#tag-extension}

Per configurare i contenuti multimediali in streaming nell’estensione tag Web SDK, segui i passaggi seguenti.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Configurare le impostazioni di **[!UICONTROL Streaming Media]** come descritto nella [pagina di configurazione dell&#39;estensione tag Web SDK](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configurare i contenuti multimediali in streaming utilizzando la libreria JavaScript dell’SDK per web {#library}

Per configurare i contenuti multimediali in streaming in Web SDK, utilizza le proprietà descritte di seguito.

Quando si chiama il comando `configure`, aggiungere l&#39;oggetto `streamingMedia`.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Proprietà | Tipo | Obbligatorio | Descrizione |
|---------|----------|---------|---------|
| `channel` | Stringa | Sì | Nome del canale in cui si verifica la raccolta di contenuti multimediali in streaming. Esempio: `Video channel`. |
| `playerName` | Stringa | Sì | Nome del lettore multimediale. |
| `appVersion` | Stringa | No | Versione dell’applicazione lettore multimediale. |
| `mainPingInterval` | Intero | No | Frequenza dei ping per il contenuto principale, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `10` e `50` secondi.  Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](../createmediasession.md#automatic). |
| `adPingInterval` | Intero | No | Frequenza dei ping per il contenuto dell’annuncio, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `1` e `10` secondi. Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizzano [sessioni con tracciamento automatico](../createmediasession.md#automatic). |
