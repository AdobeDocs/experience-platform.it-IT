---
title: Rendering di contenuti personalizzati con Adobe Experience Platform Web SDK
description: Scoprite come eseguire il rendering del contenuto personalizzato con Adobe Experience Platform Web SDK.
keywords: personalizzazione;renderingDecisions;sendEvent;DecisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Rendering di contenuti personalizzati

Adobe Experience Platform [!DNL Web SDK] supporta l&#39;esecuzione di query sulle soluzioni di personalizzazione  Adobe, incluso  Adobe Target. Esistono due modalità di personalizzazione: recupero del contenuto che può essere rappresentato automaticamente e del contenuto di cui lo sviluppatore deve eseguire il rendering. L&#39;SDK fornisce inoltre funzionalità per [gestire lo sfarfallio](../personalization/manage-flicker.md).

## Rendering automatico del contenuto

L&#39;SDK esegue automaticamente il rendering del contenuto personalizzato quando si invia un evento al server e si imposta `renderDecisions` su `true` come opzione sull&#39;evento.

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Il rendering del contenuto personalizzato è asincrono, pertanto non dovrebbe essere previsto se una particolare parte del contenuto fa parte della pagina.

## Rendering manuale del contenuto

È possibile richiedere la restituzione dell&#39;elenco di decisioni come promessa nel comando `sendEvent` specificando l&#39;opzione `decisionScopes`. Un ambito è una stringa che consente alla soluzione di personalizzazione di sapere quale decisione si desidera prendere.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Questo restituirà un elenco di decisioni come oggetto JSON per ogni decisione.

```json
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

>[!TIP]
>
> Se si utilizza [!DNL Target], gli ambiti diventano mBox sul server, solo che sono tutti richiesti contemporaneamente invece che individualmente. La mbox globale viene sempre inviata.

### Recuperare il contenuto automatico

Se si desidera che `result.decisions` includa le decisioni di rendering automatico e NON che siano sottoposte a rendering automatico, è possibile impostare `renderDecisions` su `false` e includere l&#39;ambito speciale `__view__`.
