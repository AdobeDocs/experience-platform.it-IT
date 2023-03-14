---
title: Identificazione del visitatore tramite FPID
description: Scopri come identificare in modo coerente i visitatori tramite l’API server utilizzando l’FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: rete edge;gateway;api;visitatore;identificazione;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Identificazione del visitatore tramite FPID

[!DNL First-party IDs] (`FPIDs`) sono ID dispositivo generati, gestiti e memorizzati dai clienti. Questo offre ai clienti il controllo necessario per identificare i dispositivi degli utenti. Inviando `FPIDs`, la rete Edge non genera un nuovo marchio `ECID` per una richiesta che non ne contiene una.

Il `FPID` può essere incluso nel corpo della richiesta API come parte del `identityMap` oppure può essere inviato come cookie.

Un `FPID` può essere convertito in modo deterministico in un `ECID` dalla rete Edge, quindi `FPID` Le identità di sono completamente compatibili con le soluzioni Experience Cloud. Ottenimento di un `ECID` da uno specifico `FPID` produce sempre lo stesso risultato, in modo che gli utenti abbiano un’esperienza coerente.

Il `ECID` ottenuto in questo modo può essere recuperato tramite un `identity.fetch` query:

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

Per le richieste che contengono sia `FPID` e un `ECID`, il `ECID` già presente nella richiesta avrà la precedenza su quella che potrebbe essere generata dal `FPID`. In altre parole, la rete Edge utilizza `ECID` già fornite e il `FPID` viene ignorato. Una nuova `ECID` viene generato solo quando un `FPID` viene fornito da solo.

In termini di ID dispositivo, il `server` gli stream di dati devono utilizzare `FPID` come ID dispositivo. Altre identità (ad esempio `EMAIL`) può essere fornito anche all’interno del corpo della richiesta, ma la rete Edge richiede che sia fornita esplicitamente un’identità primaria. L’identità primaria è l’identità di base in cui verranno memorizzati i dati del profilo.

>[!NOTE]
>
>Le richieste prive di identità o senza identità primaria impostata in modo esplicito nel corpo della richiesta non avranno esito negativo.

I seguenti elementi `identityMap` il gruppo di campi è formato correttamente per un `server` richiesta dello stream di dati:

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

I seguenti elementi `identityMap` gruppo di campi restituirà una risposta di errore se impostato su `server` richiesta dello stream di dati:

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

## Identificazione dei visitatori con `FPID`

Per identificare gli utenti tramite `FPID`, assicurano che `FPID` Il cookie è stato inviato prima di effettuare qualsiasi richiesta a Edge Network. Il `FPID` può essere passato in un cookie o come parte del `identityMap` nel corpo della richiesta.

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

## Richiedi con `FPID` passato come `identityMap` campo

L’esempio seguente trasmette il [!DNL FPID] come `identityMap` parametro.

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
