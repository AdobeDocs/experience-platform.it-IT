---
title: streamingMedia
description: Configura l’SDK per web per raccogliere i dati relativi all’utilizzo dei contenuti multimediali nelle proprietà web.
source-git-commit: c0cb244221215f78f9ef13d8a54a8799ab15df6c
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

Il `streamingMedia` Questo componente consente di raccogliere i dati relativi alle sessioni multimediali sul sito web.

I dati raccolti possono includere informazioni su riproduzioni multimediali, pause, completamenti e altri eventi correlati. Una volta raccolti, puoi inviare questi dati a Adobe Experience Platform e/o Adobe Analytics, per generare rapporti. Questa funzione fornisce una soluzione completa per il tracciamento e la comprensione del comportamento di consumo dei contenuti multimediali sul sito web.

## Prerequisiti {#prerequisites}

Per utilizzare `streamingMedia` componente di Web SDK, è necessario soddisfare i seguenti prerequisiti:

* Assicurati di avere accesso a Adobe Experience Platform e/o Adobe Analytics.
* È necessario utilizzare Web SDK versione 2.20.0 o successiva. Consulta la [Panoramica sull’installazione di Web SDK](../../install/overview.md) per scoprire come installare la versione più recente.
* Abilita **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** per lo stream di dati in uso.
* Assicurati che lo schema utilizzato dallo stream di dati includa i campi dello schema di Media Collection.
* Configura la funzione Streaming Media nella configurazione dell’SDK Web, come mostrato in questa pagina, tramite [estensione tag](#tag-extension) o tramite [Libreria JavaScript](#library).

## Configurare i contenuti multimediali in streaming utilizzando l’estensione tag Web SDK {#tag-extension}

Per configurare i contenuti multimediali in streaming nell’estensione tag Web SDK, segui i passaggi seguenti.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** il [!UICONTROL Adobe Experience Platform Web SDK] Card.
1. Configurare **[!UICONTROL Contenuti multimediali in streaming]** come descritto nella sezione [Pagina di configurazione dell’estensione tag Web SDK](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Configurare i contenuti multimediali in streaming utilizzando la libreria JavaScript dell’SDK per web {#library}

Per configurare i contenuti multimediali in streaming in Web SDK, utilizza le proprietà descritte di seguito.

Quando si chiama `configure` , aggiungere il comando `streamingMedia` oggetto.

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
| `mainPingInterval` | Intero | No | Frequenza dei ping per il contenuto principale, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `10` a `50` secondi.  Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizza [sessioni tracciate automaticamente](../createmediasession.md#automatic). |
| `adPingInterval` | Intero | No | Frequenza dei ping per il contenuto dell’annuncio, in secondi. Il valore predefinito è `10`. I valori possono essere compresi tra `1` a `10` secondi. Se non viene specificato alcun valore, viene utilizzato il valore predefinito quando si utilizza [sessioni tracciate automaticamente](../createmediasession.md#automatic). |
