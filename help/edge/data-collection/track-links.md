---
title: Tracciamento dei collegamenti con  Adobe Analytics
seo-title: Tracciamento dei collegamenti per  Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
seo-description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Tracciare i collegamenti

I collegamenti possono essere impostati manualmente o tracciati [automaticamente](#automaticLinkTracking). Il tracciamento manuale viene effettuato aggiungendo i dettagli nella `web.webInteraction` parte dello schema. Sono necessarie tre variabili:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
      }
    }
  }
});
```

Il tipo di collegamento può essere uno dei tre valori seguenti:

* **`other`:** Collegamento personalizzato
* **`download`:** Collegamento per il download
* **`exit`:** Collegamento di uscita

## Tracciamento automatico dei collegamenti {#automaticLinkTracking}

Per impostazione predefinita, l’SDK Web acquisisce, etichette e registra i clic su tag di collegamento idonei. I clic vengono acquisiti con un listener di eventi [Capture](https://www.w3.org/TR/uievents/#capture-phase) click associato al documento.

Il tracciamento automatico dei collegamenti può essere disabilitato [configurando](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) l&#39;SDK Web.

```javascript
clickCollectionEnabled: false
```

### Quali tag sono idonei per il tracciamento dei collegamenti?{#qualifyingLinks}

Il tracciamento automatico dei collegamenti viene eseguito per ancoraggi `A` e `AREA` tag. Tuttavia, questi tag non vengono considerati per il tracciamento dei collegamenti se dispongono di un `onclick` gestore collegato.

### Come sono etichettati i collegamenti?{#labelingLinks}

I collegamenti sono etichettati come collegamento di download se il tag di ancoraggio include un attributo di download o se il collegamento termina con un’estensione di file popolare. Il qualificatore del collegamento per il download può essere [configurato](../fundamentals/configuring-the-sdk.md) con un&#39;espressione regolare:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

I collegamenti sono etichettati come collegamento di uscita se il dominio di destinazione del collegamento è diverso da quello corrente `window.location.hostname`.

I collegamenti che non possono essere considerati come collegamenti di download o di uscita sono etichettati come &quot;altri&quot;.
