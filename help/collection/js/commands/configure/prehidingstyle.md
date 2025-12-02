---
title: prehidingStyle
description: Crea una definizione CSS che consenta il caricamento di contenuto personalizzato senza sfarfallio.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

La proprietà `prehidingStyle` ti consente di definire un selettore CSS per nascondere il contenuto personalizzato fino al caricamento. Questa proprietà è utile nelle implementazioni sincrone di Web SDK per evitare sfarfallii. Adobe consiglia di utilizzare il [frammento pre-hiding](/help/collection/use-cases/personalization/manage-flicker.md) per le implementazioni asincrone di Web SDK.

I selettori CSS definiti in questa proprietà iniziano a nascondere il contenuto quando si esegue il primo comando [`sendEvent`](../sendevent/overview.md) su una pagina. Il contenuto viene reso visibile quando viene ricevuta una risposta da Adobe, che in genere include contenuti personalizzati. Il contenuto è visibile anche se il comando `sendEvent` non riesce o si interrompe.

Se si includono sia `prehidingStyle` che il frammento pre-hiding nell&#39;implementazione, il frammento pre-hiding ha la priorità rispetto a questa proprietà di configurazione.

Impostare la stringa `prehidingStyle` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione del Web SDK, non verrà nascosto nulla durante l&#39;esecuzione del primo comando `sendEvent` in una pagina. Imposta questo valore sul selettore CSS e sul blocco di dichiarazione desiderati per le librerie caricate in modo sincrono.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Prehiding dello stile tramite l’estensione tag Web SDK

Queste impostazioni possono essere configurate nell&#39;estensione tag Web SDK utilizzando [Impostazioni di configurazione Personalization](/help/tags/extensions/client/web-sdk/configure/personalization.md).
