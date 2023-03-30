---
title: Tracciare i collegamenti tramite l’SDK per web di Adobe Experience Platform
description: Scopri come inviare dati di collegamento ad Adobe Analytics con Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;visualizzazioni di pagina;tracciamento collegamenti;collegamenti;tracciamento collegamenti;clickCollection;raccolta clic;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Tracciare i collegamenti

I collegamenti possono essere impostati manualmente o tracciati [automaticamente](#automaticLinkTracking). Il tracciamento manuale viene effettuato aggiungendo i dettagli nella sezione `web.webInteraction` parte dello schema. Sono necessarie tre variabili:

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

A partire dalla versione 2.15.0, l’SDK per web acquisisce le `region` dell’elemento HTML selezionato. Ciò abilita [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=it) funzioni di reporting in Adobe Analytics.

Il tipo di collegamento può essere uno dei tre valori seguenti:

* **`other`:** Collegamento personalizzato
* **`download`:** Collegamento di download
* **`exit`:** Collegamento di uscita

Questi valori sono [mappatura automatica](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics se [configurato](adobe-analytics/analytics-overview.md) per farlo.

## Tracciamento automatico dei collegamenti {#automaticLinkTracking}

Per impostazione predefinita, l’SDK web acquisisce, etichetta e registra i clic sui tag di collegamento idonei. I clic vengono catturati con un [catturare](https://www.w3.org/TR/uievents/#capture-phase) fare clic sul listener di eventi associato al documento.

Il tracciamento automatico dei collegamenti può essere disabilitato da [configurazione](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) SDK per web.

```javascript
clickCollectionEnabled: false
```

### Quali tag sono qualificati per il tracciamento dei collegamenti?{#qualifyingLinks}

Il tracciamento automatico dei collegamenti viene eseguito per l’ancoraggio `A` e `AREA` tag. Tuttavia, questi tag non vengono considerati per il tracciamento dei collegamenti se hanno un allegato `onclick` handler.

### Come vengono etichettati i collegamenti?{#labelingLinks}

I collegamenti sono etichettati come collegamento di download se il tag di ancoraggio include un attributo di download o se il collegamento termina con una comune estensione di file. Il qualificatore del collegamento di download può essere [configurato](../fundamentals/configuring-the-sdk.md) con espressione regolare:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

I collegamenti sono etichettati come link di uscita se il dominio di destinazione del collegamento è diverso da quello corrente `window.location.hostname`.

I collegamenti non qualificati come collegamento di download o di uscita sono etichettati come &quot;altri&quot;.

### Come si possono filtrare i valori di tracciamento dei collegamenti?

I dati raccolti con tracciamento automatico dei collegamenti possono essere ispezionati e filtrati fornendo un [funzione di callback onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Filtrare i dati di tracciamento dei collegamenti può essere utile quando si preparano i dati per il reporting di Analytics. Il tracciamento automatico dei collegamenti acquisisce sia il nome del collegamento che l’URL del collegamento. Nei rapporti di Analytics, il nome del collegamento ha priorità rispetto all’URL del collegamento. Se desideri segnalare l’URL del collegamento, devi rimuovere il nome del collegamento. L’esempio seguente mostra un `onBeforeEventSend` funzione che rimuove il nome del collegamento per i collegamenti di download:

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

A partire dalla versione 2.15.0 dell’SDK per web, i dati raccolti con il tracciamento automatico dei collegamenti possono essere ispezionati, potenziati o filtrati fornendo un [funzione di callback onBeforeLinkClickSend](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Questa funzione di callback viene eseguita solo quando si verifica un evento di clic del collegamento automatico.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Quando filtrano gli eventi di tracciamento dei collegamenti utilizzando la variabile `onBeforeLinkClickSend` Adobe consiglia di restituire `false` per i clic di collegamento che non devono essere tracciati. Qualsiasi altra risposta farà sì che l’SDK web invii i dati alla rete Edge.


>[!NOTE]
>
>** Quando entrambi i `onBeforeEventSend` e `onBeforeLinkClickSend` le funzioni di callback sono impostate, l&#39;SDK per web esegue il `onBeforeLinkClickSend` funzione di callback per filtrare e potenziare l’evento di interazione clic collegamento, seguito dalla `onBeforeEventSend` funzione di callback.