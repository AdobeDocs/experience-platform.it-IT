---
title: Interazione con Adobe Analytics
description: Scopri come utilizzare l’API server di rete Edge per interagire con Adobe Analytics
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Analytics
keywords: raccolta dei dati; uscita; analisi; API di rete Adobe Experience Platform Edge;analytics
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---

# Interazione con Adobe Analytics

## Panoramica {#overview}

La raccolta dati di Adobe Analytics funziona traducendo i dati XDM in un formato comprensibile per Adobe Analytics. Diversi campi XDM sono [mappatura automatica](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) alle variabili di Analytics.

È inoltre possibile [mappare manualmente i valori XDM](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) alle variabili Analytics legacy.

Per consentire ad Adobe Analytics di ricevere dati dall’API del server, devi [configurare il datastream](../edge/fundamentals/datastreams.md#adobe-analytics-settings) per inoltrare gli eventi ad Adobe Analytics, immettendo l’ID suite di rapporti nella pagina di configurazione del datastream.

![Configurazione di Adobe Analytics Datastream](assets/analytics-datastream.png)

## Interazione con Adobe Analytics {#interacting-analytics}

### Formato API {#format}

```http
POST https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Richiesta {#request}

L&#39;esempio seguente include diversi valori mappati automaticamente dal `_experience.analytics` gruppo di campi. Include anche livelli di dati basati su JSON. Sebbene questi livelli dati non possano essere mappati automaticamente, è possibile utilizzarli [Preparazione per la raccolta dei dati](../edge/fundamentals/datastreams.md#data-prep) per mappare questi valori su uno schema contenente gruppi di campi a cui si fa riferimento in precedenza.

Tutti i valori mappati dagli utenti a tali campi verranno automaticamente mappati ai valori Analytics appropriati, come se fossero inclusi nella richiesta API.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" \
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
