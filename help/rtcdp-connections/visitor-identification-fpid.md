---
title: Identificazione dei visitatori tramite FPID
description: Scopri come identificare in modo coerente i visitatori tramite l’API server, utilizzando il FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: rete perimetrale;gateway;api;visitatore;identificazione;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Identificazione dei visitatori tramite FPID

## Panoramica

[!DNL First-party IDs] (`FPIDs`) sono ID dispositivo generati, gestiti e memorizzati dai clienti. Questo offre ai clienti il controllo sull&#39;identificazione dei dispositivi utente. Tramite invio `FPIDs`, la rete Edge non genera un nuovo brand `ECID` per una richiesta che non ne contiene una.

La `FPID` può essere incluso nel corpo della richiesta API come parte del `identityMap` oppure può essere inviato come cookie.

Un `FPID` può essere tradotto in modo deterministico in un `ECID` da Edge Network, quindi `FPID` Le identità sono completamente compatibili con le soluzioni Experience Cloud. Ottenimento di un `ECID` da uno specifico `FPID` restituisce sempre lo stesso risultato, in modo che gli utenti abbiano un’esperienza coerente.

La `ECID` ottenuto in questo modo può essere recuperato tramite un `identity.fetch` query:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Per le richieste che contengono sia `FPID` e `ECID`, `ECID` già presente nella richiesta avrà la precedenza su quella che potrebbe essere generata dal `FPID`. Pertanto, la rete Edge utilizzerà il `ECID` già fornito e non ne calcolerà uno dal `FPID`.

In termini di ID dispositivo, la `server` i datastreams devono utilizzare `FPID` come ID dispositivo. Altre identità `EMAIL`) può essere fornito anche all’interno del corpo della richiesta, ma la rete Edge richiede che venga fornita esplicitamente un’identità primaria. L’identità principale è l’identità di base in cui verranno memorizzati i dati del profilo.

>[!NOTE]
>
>Le richieste prive di identità, rispettivamente nessuna identità principale impostata esplicitamente nel corpo della richiesta, non avranno esito positivo.

I seguenti `identityMap` formato corretto per un gruppo di campi `server` richiesta datastream:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

I seguenti `identityMap` un gruppo di campi genera una risposta di errore quando viene impostato su un `server` richiesta datastream:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

La risposta di errore restituita da Edge Network in questo caso è simile alla seguente:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Identificazione del visitatore con `FPID`

Per identificare gli utenti tramite `FPID`, assicura che `FPID` il cookie è stato inviato prima di effettuare richieste alla rete Edge. La `FPID` può essere passato in un cookie o come parte del `identityMap` nel corpo della richiesta.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
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
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## Richiesta con `FPID` passato come `identityMap` field

L&#39;esempio che segue trasmette [!DNL FPID] come `identityMap` parametro .

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
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
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
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
