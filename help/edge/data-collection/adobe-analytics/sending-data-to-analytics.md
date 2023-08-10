---
title: Invio di dati ad Adobe Analytics tramite Adobe Experience Platform Web SDK
description: Scopri come inviare dati ad Adobe Analytics utilizzando Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web interaction;visualizzazioni di pagina;tracciamento dei collegamenti;link;tracciare i collegamenti;clickCollection;click collection;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Invio di dati ad Adobe Analytics

Mentre in passato esistevano funzioni diverse per distinguere tra una visualizzazione di pagina e un collegamento (ad esempio, `s.t(), s.tl()`), nell’SDK per web è presente solo il `sendEvent` comando. I dati inviati con un evento determinano se deve essere una visualizzazione di pagina o un collegamento. [Ulteriori informazioni sul tracciamento dei collegamenti](../track-links.md).

## Invio di una visualizzazione di pagina

È possibile specificare una visualizzazione di pagina impostando `web.webPageDetails.pageViews.value=1` variabile.

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

Anche se Analytics registra tecnicamente una visualizzazione di pagina anche se questa variabile non è impostata, è consigliabile impostare questa variabile ogni volta che desideri registrare una visualizzazione di pagina in modo che sia esplicita nei dati e che sia possibile verificare l’implementazione in futuro.
