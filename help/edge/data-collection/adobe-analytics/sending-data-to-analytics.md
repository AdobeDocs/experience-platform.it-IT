---
title: Invio di dati a  Adobe Analytics tramite Adobe Experience Platform Web SDK
description: Scoprite come inviare dati ad  Adobe Analytics tramite Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;visualizzazioni di pagina;tracciamento dei collegamenti;collegamenti;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Invio di dati a  Adobe Analytics

Mentre in passato esistevano funzioni diverse per distinguere tra una visualizzazione di pagina e un collegamento (ad esempio, `s.t(), s.tl()`), nell&#39;SDK Web è presente solo il comando `sendEvent`. I dati inviati con un evento determinano se si tratta di una visualizzazione di pagina o di un collegamento. [Ulteriori informazioni sul tracciamento dei collegamenti](../track-links.md).

## Invio di una visualizzazione pagina

È possibile specificare una visualizzazione di pagina impostando la variabile `web.webPageDetails.pageViews.value=1`.

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
