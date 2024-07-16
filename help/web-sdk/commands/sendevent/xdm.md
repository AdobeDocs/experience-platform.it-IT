---
title: xdm
description: Scopri come inviare dati ad Adobe tramite l’oggetto allineato allo schema XDM.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

L&#39;oggetto `xdm` contiene il payload di dati inviato all&#39;Adobe. I campi impostati all’interno di questo oggetto vengono mappati direttamente agli elementi definiti nello schema del set di dati.

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e, quindi, ottenere valore dai dati.

Questo oggetto ha un limite massimo di 32 KB.

## Configurare l’oggetto XDM tramite l’estensione Web SDK

Imposta l&#39;oggetto **[!UICONTROL XDM]** nelle azioni di una regola di tag. L&#39;oggetto [XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) fornisce un&#39;interfaccia intuitiva per mappare altri elementi dati ai rispettivi campi XDM.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Fornisci l&#39;elemento dati contenente l&#39;oggetto desiderato nel campo **[!UICONTROL XDM]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare l’oggetto XDM utilizzando la libreria JavaScript dell’SDK per web

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
