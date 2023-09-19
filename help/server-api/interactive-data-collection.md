---
title: Raccolta interattiva di dati
description: Scopri in che modo l’API del server di rete Edge di Adobe Experience Platform esegue la raccolta interattiva dei dati.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 7%

---

# Raccolta interattiva di dati

## Panoramica {#overview}

Gli endpoint di raccolta dati interattivi ricevono un singolo evento e vengono utilizzati quando il client prevede che venga restituita una risposta dal server di rete Edge di Adobe Experience Platform. Questi endpoint possono inoltre restituire contenuto da altri servizi di rete Edge, durante l’esecuzione della raccolta dati.

La risposta del server include uno o più `Handle` come mostrato di seguito.

## Esempio di chiamata API

### Formato API {#format}

```http
POST /ee/v2/interact
```

### Richiesta {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
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
| `dataStreamId` | `String` | Sì. | ID dello stream di dati. |
| `requestId` | `String` | No | Fornisci un ID casuale client per correlare le richieste interne del server. Se non ne viene fornito alcuno, la rete Edge ne genererà uno e lo restituirà nella risposta. |

### Risposta {#response}

Una risposta corretta restituisce lo stato HTTP `200 OK`, con uno o più `Handle` a seconda dei servizi edge in tempo reale abilitati nella configurazione dello stream di dati.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
