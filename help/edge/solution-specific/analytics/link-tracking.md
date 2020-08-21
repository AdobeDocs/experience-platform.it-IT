---
title: Tracciamento di pagine e collegamenti con  Adobe Analytics
seo-title: Tracciamento dei collegamenti per  Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
seo-description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: ef01c258cb9ac72f0912d17dcd113c1baa2a5b5e
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Invio di dati a  Adobe Analytics

Mentre in passato esistevano diverse funzioni da distinguere tra una visualizzazione di pagina e un collegamento (ad esempio, `s.t(), s.tl()`), nell’SDK per Web è presente solo il `sendEvent` comando. I dati inviati con un evento determinano se si tratta di una visualizzazione di pagina o di un collegamento.

## Invio di una visualizzazione pagina

È possibile specificare una visualizzazione pagina impostando la `web.webPageDetails.pageViews.value=1` variabile.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Sebbene l&#39;analisi registri tecnicamente una visualizzazione di pagina anche se questa variabile non è impostata, è comunque consigliabile impostare questa variabile ogni volta che si desidera registrare una visualizzazione di pagina per essere esplicita nei dati e per garantire l&#39;implementazione futura.

## Tracciamento dei collegamenti

I collegamenti possono essere impostati manualmente o tracciati [automaticamente](#automaticLinkTracking). Il tracciamento manuale viene effettuato aggiungendo i dettagli nella `web.webInteraction` parte dello schema. Sono necessarie tre variabili: `web.webInteraction.name`, `web.webInteraction.type` e `web.webInteraction.linkClicks.value`.

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
});
```

Il tipo di collegamento può essere uno dei tre valori seguenti:

* **`other`:** Collegamento personalizzato
* **`download`:** Collegamento per il download
* **`exit`:** Collegamento di uscita

### Tracciamento collegamento automatico {#automaticLinkTracking}

Per impostazione predefinita, l&#39;SDK Web acquisisce, [etichette](#labelingLinks)e [record](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) fa clic su tag di collegamento [idonei](#qualifyingLinks) . I clic vengono acquisiti con un listener di eventi [Capture](https://www.w3.org/TR/uievents/#capture-phase) click associato al documento.

La disattivazione del tracciamento automatico dei collegamenti può essere effettuata [configurando](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) l’SDK per il Web.

```javascript
clickCollectionEnabled: false
```

#### Quali tag sono idonei per il tracciamento dei collegamenti?{#qualifyingLinks}

Il tracciamento automatico dei collegamenti viene eseguito per ancoraggi `A` e `AREA` tag. Tuttavia, questi tag non vengono considerati per il tracciamento dei collegamenti se dispongono di un `onclick` gestore collegato.

#### Come sono etichettati i collegamenti?{#labelingLinks}

I collegamenti sono etichettati come collegamento di download se il tag di ancoraggio include un attributo di download o se il collegamento termina con un’estensione di file popolare. Il qualificatore del collegamento per il download può essere [configurato](../../fundamentals/configuring-the-sdk.md) con un&#39;espressione regolare:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

I collegamenti sono etichettati come collegamento di uscita se il dominio di destinazione del collegamento è diverso da quello corrente `window.location.hostname`.

I collegamenti che non possono essere considerati come collegamenti di download o di uscita sono etichettati come &quot;altri&quot;.
