---
title: Raccolta dati
description: Scopri come l’API di Adobe Experience Platform Edge Network Server struttura i dati raccolti
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: raccolta dati;raccolta;Adobe Experience Platform Edge Network;api;struttura
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 7%

---


# Raccolta dati

La [!DNL Server API] offre due tipi di endpoint di raccolta dati:

* [Endpoint di raccolta dati interattivi](interactive-data-collection.md), utilizzato quando il client prevede che una risposta venga restituita dal server. Questi endpoint possono anche restituire contenuto da altri servizi di rete Edge, durante l’esecuzione della raccolta dati.
* [Raccolta di dati evento non interattivi](non-interactive-data-collection.md), utilizzato quando non è prevista alcuna risposta dal server. Questi endpoint vengono utilizzati solo per la raccolta dati.

## `Event` oggetto {#event-object}

Dati raccolti dal [!DNL Server API] è strutturato in `Event` oggetto. La struttura dell&#39;oggetto è descritta di seguito.

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
| `xdm` | Oggetto | *Obbligatorio*. Oggetto JSON contenente dati in formato XDM, corrispondente allo schema del set di dati. |
| `data` | Oggetto | *Facoltativo*. Oggetto JSON contenente dati in formato libero che possono essere mappati su XDM da Edge Network. |

