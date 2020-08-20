---
title: Tracciamento di pagine e collegamenti con  Adobe Analytics
seo-title: Tracciamento dei collegamenti per  Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
seo-description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '236'
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

I collegamenti possono essere impostati aggiungendo i dettagli nella `web.webInteraction` parte dello schema. Sono necessarie tre variabili: `web.webInteraction.name`, `web.webInteraction.type` e `web.webInteraction.linkClicks.value`.

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
* **`download`:** Un collegamento per il download (che può essere tracciato automaticamente dalla libreria)
* **`exit`:** Collegamento di uscita

### Tracciamento collegamento automatico

L&#39;SDK Web può tracciare automaticamente tutti i clic dei collegamenti attivando [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled).

I collegamenti di download vengono rilevati automaticamente in base ai tipi di file più comuni. La logica per la classificazione dei download è configurabile.
