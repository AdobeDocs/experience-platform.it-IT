---
title: documentUnloading
description: Utilizza l’API sendBeacon di JavaScript per inviare dati ad Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

La proprietà `documentUnloading` consente di utilizzare il metodo [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) di JavaScript per inviare dati ad Adobe. Se una richiesta tipica richiede troppo tempo, il browser può annullarla. È possibile indicare al Web SDK di utilizzare `sendBeacon` in modo che la richiesta venga eseguita in background dopo l&#39;uscita dalla pagina. Abilita questa proprietà per evitare che le richieste di dati vengano annullate dal browser durante lo scaricamento.

Diversi browser impongono un limite di 64 KB alla quantità di dati che è possibile inviare contemporaneamente con `sendBeacon`. Se il browser rifiuta l’evento perché il payload è troppo grande, il Web SDK utilizza il normale metodo di trasporto. Anche se un determinato browser consente payload più grandi, i server di raccolta dati di Adobe troncano i payload fino a 64 KB.

Impostare il valore booleano `documentUnloading` durante l&#39;esecuzione del comando `sendEvent`. Il valore predefinito è `false`. Impostare questa proprietà su `true` se si desidera utilizzare il metodo `sendBeacon` per inviare dati ad Adobe.

>[!IMPORTANT]
>
>La proprietà `documentUnloading` non è compatibile con la proprietà [`renderDecisions`](renderdecisions.md). Evitare di impostare entrambe le proprietà su `true` contemporaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Scaricamento del documento tramite l’estensione tag Web SDK

La casella di controllo **[!UICONTROL Document will unload]** è disponibile durante la configurazione di un&#39;azione [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) quando si utilizza l&#39;estensione tag Web SDK.
