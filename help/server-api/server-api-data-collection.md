---
title: Raccolta dati
description: Scopri come l’API Adobe Experience Platform Edge Network Server struttura i dati raccolti.
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---


# Raccolta dati

[!DNL Server API] offre due tipi di endpoint di raccolta dati:

* [Endpoint di raccolta dati interattivi](interactive-data-collection.md), utilizzati quando il client prevede che venga restituita una risposta dal server. Durante la raccolta dei dati, questi endpoint possono restituire anche il contenuto di altri servizi Edge Network.
* [Raccolta dati evento non interattiva](non-interactive-data-collection.md), utilizzata quando non è prevista alcuna risposta dal server. Questi endpoint vengono utilizzati solo per la raccolta di dati.

## `Event` oggetto {#event-object}

I dati raccolti da [!DNL Server API] sono strutturati nell&#39;oggetto `Event`. La struttura di questo oggetto è descritta di seguito.

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Attributo | Tipo | Descrizione |
| --- | --- | --- |
| `xdm` | Oggetto | *Richiesto*. Oggetto JSON contenente dati in formato XDM, corrispondente allo schema del set di dati. |
| `data` | Oggetto | *Facoltativo*. Oggetto JSON contenente dati in formato libero, che può essere mappato a XDM dall’Edge Network. |

