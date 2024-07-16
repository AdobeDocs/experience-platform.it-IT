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

[!DNL First-party IDs] (`FPIDs`) sono ID dispositivo generati, gestiti e archiviati dai clienti. Questo offre ai clienti il controllo necessario per identificare i dispositivi degli utenti. Inviando `FPIDs`, l&#39;Edge Network non genera un `ECID` nuovo per una richiesta che non ne contiene uno.

`FPID` può essere incluso nel corpo della richiesta API come parte di `identityMap` oppure può essere inviato come cookie.

Un oggetto `FPID` può essere convertito in modo deterministico in un oggetto `ECID` dall&#39;Edge Network, pertanto le identità `FPID` sono completamente compatibili con le soluzioni Experience Cloud. Ottenere un `ECID` da un `FPID` specifico produce sempre lo stesso risultato, quindi gli utenti avranno un&#39;esperienza coerente.

Il `ECID` ottenuto in questo modo può essere recuperato tramite una query `identity.fetch`:

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

Per le richieste che contengono sia un `FPID` che un `ECID`, il `ECID` già presente nella richiesta avrà la precedenza su quello che potrebbe essere generato da `FPID`. In altre parole, l&#39;Edge Network utilizza `ECID` già fornito e `FPID` viene ignorato. Un nuovo `ECID` viene generato solo quando viene fornito un `FPID`.

In termini di ID dispositivo, gli stream di dati `server` devono utilizzare `FPID` come ID dispositivo. È possibile fornire altre identità (ad esempio `EMAIL`) all&#39;interno del corpo della richiesta, ma l&#39;Edge Network richiede che venga fornita esplicitamente un&#39;identità primaria. L’identità primaria è l’identità di base in cui verranno memorizzati i dati del profilo.

>[!NOTE]
>
>Le richieste prive di identità o senza identità primaria impostata in modo esplicito nel corpo della richiesta non avranno esito negativo.

Il seguente gruppo di campi `identityMap` è formato correttamente per una richiesta dello stream di dati `server`:

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

Il seguente gruppo di campi `identityMap` restituirà una risposta di errore se impostato in una richiesta dello stream di dati `server`:

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

La risposta di errore restituita dall’Edge Network in questo caso è simile alla seguente:

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

Per identificare gli utenti tramite `FPID`, accertati che il cookie `FPID` sia stato inviato prima di effettuare qualsiasi richiesta all&#39;Edge Network. `FPID` può essere passato in un cookie o come parte di `identityMap` nel corpo della richiesta.

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

## Richiesta con `FPID` passata come campo `identityMap`

L&#39;esempio seguente passa [!DNL FPID] come parametro `identityMap`.

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
