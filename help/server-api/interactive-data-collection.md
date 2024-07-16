---
title: Raccolta interattiva di dati
description: Scopri in che modo l’API Adobe Experience Platform Edge Network Server esegue la raccolta interattiva dei dati.
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# Raccolta interattiva di dati

## Panoramica {#overview}

Gli endpoint di raccolta dati interattivi ricevono un singolo evento e vengono utilizzati quando il client prevede che venga restituita una risposta dal server di Edge Network di Adobe Experience Platform. Durante la raccolta dei dati, questi endpoint possono restituire anche il contenuto di altri servizi Edge Network.

>[!IMPORTANT]
>
>L&#39;endpoint `/interact` è progettato principalmente per essere utilizzato dagli SDK Experience Platform. Questo endpoint è soggetto a cambiamenti aggiuntivi e il suo comportamento può evolvere senza preavviso. Ad esempio, nuovi elementi potrebbero essere aggiunti al payload di risposta in futuro.

La risposta del server include uno o più oggetti `Handle`, come illustrato di seguito.

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
| `requestId` | `String` | No | Fornisci un ID casuale client per correlare le richieste interne del server. Se non viene fornito nessuno, l’Edge Network ne genera uno e lo restituisce nella risposta. |

### Risposta {#response}

In caso di esito positivo, la risposta restituisce lo stato HTTP `200 OK`, con uno o più oggetti `Handle`, a seconda dei servizi edge in tempo reale abilitati nella configurazione dello stream di dati.

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
