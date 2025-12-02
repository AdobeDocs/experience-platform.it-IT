---
title: renderDecisions
description: Esegui il rendering di contenuti personalizzati idonei per il rendering automatico.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

La proprietà `renderDecisions` consente di forzare il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico in Web SDK.

Impostare il valore booleano `renderDecisions` durante l&#39;esecuzione del comando `sendEvent`. Se omesso, il valore predefinito di questa proprietà sarà `false`. Impostare questa proprietà su `true` per eseguire automaticamente il rendering del contenuto personalizzato.

>[!IMPORTANT]
>
>La proprietà `renderDecisions` non è compatibile con la proprietà [`documentUnloading`](documentunloading.md). Evitare di impostare entrambe le proprietà su `true` contemporaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Quando si imposta questa proprietà su `true`, assicurarsi di includere anche gli ambiti o le superfici associati. Questi ambiti o superfici possono essere richiesti automaticamente (ad esempio nel primo comando `sendEvent` di una pagina) o esplicitamente (utilizzando [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) o [`personalization.surfaces`](personalization.md#personalizationsurfaces)). Un problema comune durante il rendering della personalizzazione è il seguente scenario:

1. Un comando `sendEvent` viene eseguito in anticipo sulla pagina che richiede la personalizzazione predefinita con `renderDecisions` non impostato (impostazione predefinita: `false`). Le proposte vengono recuperate ma non sottoposte a rendering.
1. Più avanti nella pagina, un altro `sendEvent` trigger con `renderDecisions` impostato su `true` ma non include ambiti o superfici. Poiché in questa seconda chiamata non sono presenti ambiti o superfici, non viene eseguito il rendering di nulla.

Per evitare questo problema:

* Impostazione di `renderDecisions` su `true` nella prima chiamata di `sendEvent`; o
* Impostazione esplicita di `decisionScopes` o `surfaces` in una chiamata `sendEvent` successiva quando si imposta `renderDecisions` su `true`.

## Eseguire il rendering delle decisioni tramite l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questa proprietà è la casella di controllo [**Decisioni di personalizzazione visiva**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) nell&#39;azione &#39;[!UICONTROL Send event]&#39;.
