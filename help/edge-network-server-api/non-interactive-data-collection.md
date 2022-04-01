---
title: Raccolta dati non interattiva
description: Scopri come l’API di Adobe Experience Platform Edge Network Server esegue la raccolta dati non interattiva
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs non-interactive data collection
keywords: raccolta dati;raccolta;rete Edge di adobe experience platform;api;raccolta dati non interattiva
source-git-commit: 3bb73e5798d8fcdb6bb8bdcb796e8df6a1bd8805
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# Raccolta dati non interattiva

## Panoramica {#overview}

Gli endpoint di raccolta dati evento non interattivi vengono utilizzati per inviare più eventi a set di dati di Experience Platform o ad altri punti vendita.

L’invio di eventi in batch è consigliato quando gli eventi dell’utente finale vengono messi in coda localmente per un breve periodo di tempo (ad esempio, in assenza di connessione di rete).

Gli eventi batch non devono necessariamente appartenere allo stesso utente finale, il che significa che gli eventi possono contenere identità diverse all’interno dei rispettivi `identityMap` oggetto.


<!-- However, when an `ECID` identity is sent via a cookie or metadata (in Edge Network accepted format), the Edge Network will read it and associate it with each event in the batch.

Each event should include the corresponding `XDM` content that needs to be collected.

>[!NOTE]
>
>[Experience Edge Identity Protocol](visitor-identification.md#experience-edge-identity-protocol) (`ECID` generation) is not applicable for data collection requests, meaning that events sent to this API should already have at least one identity associated to them. For server datastreams (calls to `server.adobedc.net`), the API requires that each event contains an identity **explicitly set as primary**. For device datastreams, the Edge Network will attempt to set the `ECID` as primary, when it is present, and no other primary identity is explicitly set.

-->

## Esempio di chiamata API non interattiva {#example}

### Formato API {#api-format}

```http
POST /ee/v2/collect
```

### Richiesta {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {IMS_ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
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
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sì | ID del datastream utilizzato dall&#39;endpoint di raccolta dati. |
| `requestId` | `String` | No | Fornisci un ID di traccia della richiesta esterna. Se non ne viene fornito nessuno, la rete Edge ne genererà uno per te e lo restituirà nel corpo o nelle intestazioni di risposta. |
| `silent` | `Boolean` | No | Parametro booleano facoltativo che indica se la rete Edge deve restituire un `204 No Content` con un payload vuoto o meno. Gli errori critici vengono segnalati utilizzando il codice di stato HTTP e il payload corrispondenti. |


### Risposta {#response}

Una risposta corretta restituisce uno degli stati seguenti e un `requestID` se non ne è stato fornito nessuno nella richiesta.

* `202 Accepted` quando la richiesta è stata elaborata con successo;
* `204 No Content` quando la richiesta è stata elaborata correttamente e il `silent` è stato impostato su `true`;
* `400 Bad Request` quando la richiesta non è stata formata correttamente (ad esempio, l’identità principale obbligatoria non è stata trovata).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
