---
title: Interazione con Adobe Analytics
description: Scopri come utilizzare l’API del server di rete Edge per interagire con Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Interazione con Adobe Analytics

## Panoramica {#overview}

La raccolta dati di Adobe Analytics funziona traducendo i dati XDM in un formato comprensibile ad Adobe Analytics. Diversi campi XDM sono [mappato automaticamente](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) alle variabili di Analytics.

È inoltre possibile [mappare manualmente i valori XDM](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) alle variabili Analytics legacy.

Per abilitare Adobe Analytics alla ricezione di dati dall’API server, devi [configurare lo stream di dati](../datastreams/overview.md#adobe-analytics-settings) per inoltrare gli eventi ad Adobe Analytics, inserendo l’ID suite di rapporti nella pagina di configurazione dello stream di dati.

![Configurazione dello stream di dati Adobe Analytics](assets/analytics-datastream.png)

## Interazione con Adobe Analytics {#interacting-analytics}

### Formato API {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Richiesta {#request}

L’esempio seguente include diversi valori mappati automaticamente dall’ `_experience.analytics` gruppo di campi. Include anche livelli di dati basati su JSON. Anche se questi livelli di dati non possono essere mappati automaticamente, è possibile utilizzare [Preparazione per la raccolta dati](../datastreams/data-prep.md) per mappare questi valori a uno schema che contiene i gruppi di campi a cui si fa riferimento in precedenza.

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
