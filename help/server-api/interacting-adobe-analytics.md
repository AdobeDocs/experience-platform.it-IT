---
title: Interazione con Adobe Analytics
description: Scopri come utilizzare l’API server di Edge Network per interagire con Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Interazione con Adobe Analytics

## Panoramica {#overview}

La raccolta dati di Adobe Analytics funziona traducendo i dati XDM in un formato comprensibile ad Adobe Analytics. Diversi campi XDM sono [mappati automaticamente](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) alle variabili di Analytics. Puoi anche mappare manualmente i valori XDM sulle variabili Analytics precedenti.

Per consentire ad Adobe Analytics di ricevere dati dall&#39;API server, devi [configurare lo stream di dati](../datastreams/overview.md#adobe-analytics-settings) per inoltrare eventi ad Adobe Analytics, immettendo l&#39;ID suite di rapporti nella pagina di configurazione dello stream di dati.

![Configurazione Adobe Analytics Datastream](assets/analytics-datastream.png)

## Interazione con Adobe Analytics {#interacting-analytics}

### Formato API {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Richiesta {#request}

L&#39;esempio seguente include diversi valori mappati automaticamente dal gruppo di campi `_experience.analytics`. Include anche livelli di dati basati su JSON. Anche se questi livelli di dati non possono essere mappati automaticamente, è possibile utilizzare [Preparazione dati per raccolta dati](../datastreams/data-prep.md) per mappare questi valori a uno schema che contiene i gruppi di campi di cui sopra.

Tutti i valori mappati dagli utenti a tali campi verranno automaticamente mappati sui valori Analytics appropriati, come se fossero inclusi nella richiesta API.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### Risposta {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
