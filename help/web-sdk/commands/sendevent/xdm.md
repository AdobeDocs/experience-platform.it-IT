---
title: xdm
description: Oggetto allineato allo schema inviato all’Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# `xdm`

Il `xdm` L&#39;oggetto contiene il payload di dati inviato all&#39;Adobe. I campi impostati all’interno di questo oggetto vengono mappati direttamente agli elementi definiti nello schema del set di dati.

Adobe Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile. Definendo i dati in modo coerente tra i sistemi, diventa più semplice mantenere un significato e, quindi, ottenere valore dai dati.

Questo campo ha un limite massimo di 32 KB.

## Configurare l’oggetto XDM tramite l’estensione Web SDK

Imposta il **[!UICONTROL XDM]** nelle azioni di una regola di tag. Il [Oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) fornisce un’interfaccia intuitiva per mappare altri elementi dati ai rispettivi campi XDM.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Fornisci l’elemento dati contenente l’oggetto desiderato nella **[!UICONTROL XDM]** campo.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare l’oggetto XDM utilizzando la libreria JavaScript dell’SDK web

Imposta il `xdm` oggetto durante l&#39;esecuzione di `sendEvent` comando. Assicurati che la gerarchia in questo oggetto corrisponda allo schema per il set di dati configurato. Puoi includere entrambi `xdm` oggetto e [`data`](data.md) oggetto nello stesso `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Nell&#39;esempio seguente viene utilizzato [Gruppo di campi schema Dettagli commerciali](/help/xdm/field-groups/event/commerce-details.md):

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
