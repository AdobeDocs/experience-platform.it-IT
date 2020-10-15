---
title: Tracciamento di pagine e collegamenti con  Adobe Analytics
seo-title: Tracciamento dei collegamenti per  Adobe Analytics con Adobe Experience Platform Web SDK
description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
seo-description: Scopri come inviare dati collegamento a  Adobe Analytics con  Experience Platform Web SDK
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Invio di dati a  Adobe Analytics

Mentre in passato esistevano funzioni diverse per distinguere tra una visualizzazione di pagina e un collegamento (ad esempio, `s.t(), s.tl()`), nell’SDK Web è presente solo il `sendEvent` comando. I dati inviati con un evento determinano se si tratta di una visualizzazione di pagina o di un collegamento. [Ulteriori informazioni sul tracciamento dei collegamenti](../track-links.md)

## Invio di una visualizzazione pagina

È possibile specificare una visualizzazione pagina impostando la `web.webPageDetails.pageViews.value=1` variabile.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Sebbene Analytics registri tecnicamente una visualizzazione di pagina anche se questa variabile non è impostata, è comunque consigliabile impostare questa variabile ogni volta che si desidera registrare una visualizzazione di pagina in modo che sia esplicita nei dati e che sia provata in futuro l’implementazione.
