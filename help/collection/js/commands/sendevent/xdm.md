---
title: xdm
description: Scopri come inviare dati ad Adobe tramite l’oggetto allineato allo schema XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

L&#39;oggetto `xdm` contiene il payload di dati inviato ad Adobe. I campi impostati all’interno di questo oggetto vengono mappati direttamente agli elementi definiti nello schema del set di dati.

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e, quindi, ottenere valore dai dati.

Impostare l&#39;oggetto `xdm` durante l&#39;esecuzione del comando `sendEvent`. Assicurati che la gerarchia in questo oggetto corrisponda allo schema per il set di dati configurato. È possibile includere sia l&#39;oggetto `xdm` che l&#39;oggetto [`data`](data.md) nello stesso comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Nell&#39;esempio seguente viene utilizzato il gruppo di campi dello schema [Dettagli Commerce](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```

## Utilizza l&#39;oggetto `xdm` tramite l&#39;estensione tag Web SDK

L&#39;oggetto `xdm` è disponibile come [elemento dati variabile](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) o [elemento dati oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) quando si utilizza l&#39;estensione tag Web SDK. Nella maggior parte dei casi, Adobe consiglia di utilizzare un elemento dati variabile.
