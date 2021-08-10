---
title: Tracciare i collegamenti tramite l’SDK per web di Adobe Experience Platform
description: Scopri come inviare dati di collegamento ad Adobe Analytics con Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;visualizzazioni di pagina;tracciamento collegamenti;collegamenti;tracciamento collegamenti;clickCollection;raccolta clic;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: d6460e442a136bf9bd26582f228017a6fb52138c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Tracciare i collegamenti

I collegamenti possono essere impostati manualmente o tracciati [automaticamente](#automaticLinkTracking). Il tracciamento manuale viene eseguito aggiungendo i dettagli nella parte `web.webInteraction` dello schema. Sono necessarie tre variabili:

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
        }
      },
      "name": "My Custom Link", // Name that shows up in the custom links report
      "URL": "https://myurl.com", // The URL of the link
      "type": "other" // values: other, download, exit
    }
  }
});
```

Il tipo di collegamento può essere uno dei tre valori seguenti:

* **`other`:** Collegamento personalizzato
* **`download`:** Collegamento per il download
* **`exit`:** Collegamento di uscita

Questi valori sono [mappati automaticamente](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics se [configurato](adobe-analytics/analytics-overview.md) per farlo.

## Tracciamento automatico dei collegamenti {#automaticLinkTracking}

Per impostazione predefinita, l’SDK web acquisisce, etichetta e registra i clic sui tag di collegamento idonei. I clic vengono acquisiti con un listener di eventi di clic [cattura](https://www.w3.org/TR/uievents/#capture-phase) allegato al documento.

Il tracciamento automatico dei collegamenti può essere disabilitato [configurando](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) l&#39;SDK per web.

```javascript
clickCollectionEnabled: false
```

### Quali tag sono qualificati per il tracciamento dei collegamenti?{#qualifyingLinks}

Il tracciamento automatico dei collegamenti viene eseguito per i tag di ancoraggio `A` e `AREA` . Tuttavia, questi tag non vengono considerati per il tracciamento dei collegamenti se dispongono di un gestore `onclick` allegato.

### Come vengono etichettati i collegamenti?{#labelingLinks}

I collegamenti sono etichettati come collegamento di download se il tag di ancoraggio include un attributo di download o se il collegamento termina con una comune estensione di file. Il qualificatore di collegamento per il download può essere [configurato](../fundamentals/configuring-the-sdk.md) con un&#39;espressione regolare:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

I collegamenti sono etichettati come collegamento di uscita se il dominio di destinazione del collegamento è diverso dal dominio corrente `window.location.hostname`.

I collegamenti non qualificati come collegamento di download o di uscita sono etichettati come &quot;altri&quot;.

### Come si possono filtrare i valori di tracciamento dei collegamenti?

I dati raccolti con tracciamento automatico dei collegamenti possono essere ispezionati e filtrati fornendo una funzione di callback [onBeforeEventSend](../fundamentals/tracking-events.md#modifying-events-globally).

Filtrare i dati di tracciamento dei collegamenti può essere utile quando si preparano i dati per il reporting di Analytics. Il tracciamento automatico dei collegamenti acquisisce sia il nome del collegamento che l’URL del collegamento. Nei rapporti di Analytics, il nome del collegamento ha priorità rispetto all’URL del collegamento. Se desideri segnalare l’URL del collegamento, devi rimuovere il nome del collegamento. L&#39;esempio seguente mostra una funzione `onBeforeEventSend` che rimuove il nome del collegamento per i collegamenti per il download:

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

