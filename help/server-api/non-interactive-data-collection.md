---
title: Raccolta di dati non interattivi
description: Scopri in che modo l’API del server di rete Edge di Adobe Experience Platform esegue la raccolta dati non interattiva.
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---


# Raccolta di dati non interattivi

## Panoramica {#overview}

Gli endpoint di raccolta dati per eventi non interattivi vengono utilizzati per inviare più eventi a set di dati Experienci Platform o ad altre prese.

L’invio di eventi in batch è consigliato quando gli eventi dell’utente finale vengono messi in coda localmente per un breve periodo di tempo (ad esempio quando non vi è alcuna connessione di rete).

Gli eventi batch non devono necessariamente appartenere allo stesso utente finale, il che significa che possono contenere identità diverse all’interno del `identityMap` oggetto.

## Esempio di chiamata API non interattiva {#example}

### Formato API {#api-format}

```http
POST /ee/v2/collect
```

### Richiesta {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
| `dataStreamId` | `String` | Sì | ID dello stream di dati utilizzato dall’endpoint di raccolta dati. |
| `requestId` | `String` | No | Specifica un ID di traccia della richiesta esterno. Se non ne viene fornito alcuno, la rete Edge ne genererà uno per te e lo restituirà nel corpo/nelle intestazioni della risposta. |
| `silent` | `Boolean` | No | Parametro booleano facoltativo che indica se la rete Edge deve restituire un `204 No Content` risposta con un payload vuoto o meno. Gli errori critici vengono segnalati utilizzando il codice di stato HTTP e il payload corrispondenti. |

### Risposta {#response}

In caso di esito positivo, la risposta restituisce uno dei seguenti stati, e un `requestID` se nella richiesta non è stata fornita alcuna informazione.

* `202 Accepted` quando la richiesta è stata elaborata correttamente;
* `204 No Content` quando la richiesta è stata elaborata correttamente e il `silent` parametro impostato su `true`;
* `400 Bad Request` quando la richiesta non era formata correttamente (ad esempio, non è stata trovata l’identità primaria obbligatoria).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
