---
title: Rendering di contenuti personalizzati
seo-title: Adobe Experience Platform Web SDK Rendering del contenuto personalizzato
description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK
seo-description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Panoramica delle opzioni di personalizzazione

Adobe Experience Platform [!DNL Web SDK] supporta la query sulle soluzioni di personalizzazione  Adobe, incluso  Adobe Target. Esistono due modalità di personalizzazione: recupero del contenuto che può essere rappresentato automaticamente e del contenuto di cui lo sviluppatore deve eseguire il rendering. L’SDK fornisce inoltre le strutture per [gestire lo sfarfallio](../../edge/solution-specific/target/flicker-management.md).

## Rendering automatico del contenuto

L’SDK esegue automaticamente il rendering del contenuto personalizzato quando si invia un evento al server e si imposta `renderDecisions` come opzione `true` sull’evento.

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

È possibile richiedere la restituzione dell&#39;elenco di decisioni come promessa nel `sendEvent` comando specificando l&#39; `decisionScopes` opzione. Un ambito è una stringa che consente alla soluzione di personalizzazione di sapere quale decisione si desidera prendere.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  })
```

Questo restituirà un elenco di decisioni come oggetto JSON per ogni decisione.

```javascript
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

### Recupera contenuto automatico

Se desiderate che il modulo `result.decisions` includa le decisioni di rendering automatico e NON disponga del rendering automatico di ALLEY, potete impostare `renderDecisions` su `false`e includere l&#39;ambito speciale `__view__`.
