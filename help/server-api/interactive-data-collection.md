---
title: Raccolta dati interattiva
description: Scopri come l’API di Adobe Experience Platform Edge Network Server esegue la raccolta dati interattiva
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: raccolta dati;raccolta;rete Edge di experience platform;api;raccolta dati interattiva
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 7%

---

# Raccolta dati interattiva

## Panoramica {#overview}

Gli endpoint di raccolta dati interattivi ricevono un singolo evento e vengono utilizzati quando il client prevede che una risposta venga restituita dal server di rete Adobe Experience Platform Edge. Questi endpoint possono anche restituire contenuto da altri servizi Experience Edge durante l’esecuzione della raccolta dati.

La risposta del server include uno o più `Handle` come illustrato di seguito.

## Esempio di chiamata API

### Formato API {#format}

```http
POST /ee/v2/interact
```

### Richiesta {#request}

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
               }
            ]
         },
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev/",
               "name": "home-demo-Home Page"
            }
         },
         "timestamp": "2021-08-09T14:09:20.859Z"
      },
      "data": {
         "prop1": "custom value"
      }
   }
}'
```

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sì. | ID Datastream. |
| `requestId` | `String` | No | Fornisci un ID casuale client per le richieste server interne correlate. Se non ne viene fornito nessuno, la rete Edge ne genererà uno e lo restituirà nella risposta. |

### Risposta {#response}

Una risposta corretta restituisce lo stato HTTP `200 OK`, con uno o più `Handle` a seconda dei servizi edge in tempo reale abilitati nella configurazione del datastream.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
