---
title: Rendering di contenuti personalizzati
seo-title: ' Adobe Experience Platform Web SDK Rendering del contenuto personalizzato'
description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK
seo-description: Scopri come eseguire il rendering del contenuto personalizzato con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 5f263a2593cdb493b5cd48bc0478379faa3e155d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Panoramica delle opzioni di personalizzazione

L&#39;SDK Web per  Adobe Experience Platform supporta la query delle soluzioni di personalizzazione in Adobe, incluso  Adobe Target. Esistono due modalità di personalizzazione: recupero del contenuto che può essere rappresentato automaticamente e del contenuto di cui lo sviluppatore deve eseguire il rendering. L’SDK fornisce inoltre le strutture per [gestire lo sfarfallio](../../edge/solution-specific/target/flicker-management.md).

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

È possibile richiedere la restituzione dell&#39;elenco di decisioni come promessa sul `event` comando utilizzando `scopes`. Un ambito è una stringa che consente alla soluzione di personalizzazione di sapere quale decisione si desidera prendere.

```javascript
alloy("sendEvent",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
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
> Se usi gli ambiti Target diventano mBox sul server, solo queste sono tutte richieste contemporaneamente anziché singolarmente. La mbox globale viene sempre inviata.

### Recupera contenuto automatico

Se desiderate che il modulo `result.decisions` includa le decisioni di rendering automatico, potete impostare `renderDecisions` su false e includere l&#39;ambito speciale `__view__`.
