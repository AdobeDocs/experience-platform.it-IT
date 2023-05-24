---
title: Tracciare i collegamenti tramite Adobe Experience Platform Web SDK
description: Scopri come inviare dati di collegamento ad Adobe Analytics con Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web interaction;visualizzazioni di pagina;tracciamento dei collegamenti;link;tracciare i collegamenti;clickCollection;click collection;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Tracciare i collegamenti

I collegamenti possono essere impostati manualmente o tracciati [automaticamente](#automaticLinkTracking). Il tracciamento manuale viene eseguito aggiungendo i dettagli sotto `web.webInteraction` parte dello schema. Sono necessarie tre variabili:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

A partire dalla versione 2.15.0, Web SDK acquisisce `region` dell’elemento HTML selezionato. In questo modo è possibile [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=it) funzionalità di reporting di Adobe Analytics.

Il tipo di collegamento può essere uno dei tre valori seguenti:

* **`other`:** Un collegamento personalizzato
* **`download`:** Un collegamento per il download
* **`exit`:** Un collegamento di uscita

Questi valori sono [mappato automaticamente](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics se [configurato](adobe-analytics/analytics-overview.md) per farlo.

## Tracciamento automatico dei collegamenti {#automaticLinkTracking}

Per impostazione predefinita, Web SDK acquisisce, etichetta e record e fa clic sui tag di collegamento qualificati. I clic vengono acquisiti con una [acquisire](https://www.w3.org/TR/uievents/#capture-phase) fare clic sul listener di eventi allegato al documento.

Il tracciamento automatico dei collegamenti può essere disabilitato da [configurazione](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) SDK per web.

```javascript
clickCollectionEnabled: false
```

### Quali tag sono idonei per il tracciamento dei collegamenti?{#qualifyingLinks}

Tracciamento automatico dei collegamenti eseguito per l&#39;ancoraggio `A` e `AREA` tag. Tuttavia, questi tag non vengono considerati per il tracciamento dei collegamenti se dispongono di un allegato `onclick` handler.

### Come vengono etichettati i collegamenti?{#labelingLinks}

I collegamenti sono etichettati come collegamento di download se il tag di ancoraggio include un attributo di download o se il collegamento termina con un’estensione di file comune. Il qualificatore del collegamento di download può essere [configurato](../fundamentals/configuring-the-sdk.md) con un’espressione regolare:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

I collegamenti sono etichettati come collegamento di uscita se il dominio di destinazione del collegamento è diverso dall’attuale `window.location.hostname`.

I collegamenti che non sono idonei come collegamento di download o di uscita sono etichettati come &quot;altro&quot;.

### Come possono essere filtrati i valori di tracciamento dei collegamenti?

I dati raccolti con il tracciamento automatico dei collegamenti possono essere ispezionati e filtrati fornendo un [funzione di callback onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Il filtraggio dei dati di tracciamento dei collegamenti può essere utile durante la preparazione dei dati per i rapporti di Analytics. Il tracciamento automatico dei collegamenti acquisisce sia il nome del collegamento che l’URL del collegamento. Nei rapporti di Analytics, il nome del collegamento ha la priorità sull’URL del collegamento. Se desideri segnalare l’URL del collegamento, devi rimuovere il nome del collegamento. L’esempio seguente mostra un’ `onBeforeEventSend` funzione che rimuove il nome del collegamento per i collegamenti di download:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

A partire dalla versione 2.15.0 dell’SDK per web, i dati raccolti con il tracciamento automatico dei collegamenti possono essere ispezionati, incrementati o filtrati fornendo un’ [funzione di callback onBeforeLinkClickSend](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Questa funzione di callback viene eseguita solo quando si verifica un evento di clic di collegamento automatico.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Quando si filtrano gli eventi di tracciamento dei collegamenti utilizzando `onBeforeLinkClickSend` , l&#39;Adobe consiglia di restituire `false` per i clic del collegamento che non devono essere tracciati. Qualsiasi altra risposta farà sì che Web SDK invii i dati alla rete Edge.


>[!NOTE]
>
>** Quando entrambe le opzioni `onBeforeEventSend` e `onBeforeLinkClickSend` funzioni di callback impostate, Web SDK esegue `onBeforeLinkClickSend` funzione di callback per filtrare e potenziare l’evento di clic sul collegamento, seguito dalla `onBeforeEventSend` callback.