---
title: Panoramica di Personalization
description: Scopri come utilizzare l’API Adobe Experience Platform Edge Network Server per recuperare contenuti personalizzati dalle soluzioni di personalizzazione Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: ae6c6d21b1eea900d01be3287827296071429d30
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 10%

---

# Panoramica di Personalization

Con [!DNL Server API], puoi recuperare contenuti personalizzati dalle soluzioni di personalizzazione Adobe, tra cui [Adobe Target](https://business.adobe.com/it/products/target/adobe-target.html), [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) e [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=it).

Inoltre, [!DNL Server API] potenzia le funzionalità di personalizzazione della stessa pagina e della pagina successiva tramite destinazioni di personalizzazione Adobe Experience Platform, come [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) e la [connessione di personalizzazione personalizzata](../destinations/catalog/personalization/custom-personalization.md). Per informazioni su come configurare Experience Platform per la personalizzazione della stessa pagina e della pagina successiva, consulta la [guida dedicata](../destinations/ui/activate-edge-personalization-destinations.md).

Quando utilizzi l’API server, devi integrare la risposta fornita dal motore di personalizzazione con la logica utilizzata per eseguire il rendering del contenuto sul sito. A differenza di [Web SDK](../web-sdk/home.md), [!DNL Server API] non dispone di un meccanismo per applicare automaticamente il contenuto restituito dalle soluzioni di personalizzazione Adobe.

## Terminologia {#terminology}

Prima di lavorare con le soluzioni di personalizzazione Adobe, assicurati di comprendere i seguenti concetti:

* **Offerta**: un’offerta è un messaggio di marketing a cui possono essere associate delle regole volte a determinare gli utenti idonei che potranno visualizzare l’offerta.
* **Decisione**: una decisione (precedentemente nota come attività di offerta) informa la selezione di un&#39;offerta.
* **Schema**: lo schema di una decisione informa il tipo di offerta restituito.
* **Ambito**: ambito della decisione.
   * In Adobe Target, è [!DNL mbox]. [!DNL global mbox] è l&#39;ambito `__view__`
   * Per [!DNL Offer Decisioning], si tratta delle stringhe con codifica Base64 di JSON contenenti gli ID di attività e posizionamento che il servizio offer decisioning deve utilizzare per proporre le offerte.

## Oggetto `query` {#query-object}

Il recupero di contenuto personalizzato richiede un oggetto query di richiesta esplicito per un esempio di richiesta. L’oggetto query ha il seguente formato:

```json
{
  "query": {
    "personalization": {
      "schemas": [
        "https://ns.adobe.com/personalization/html-content-item",
        "https://ns.adobe.com/personalization/json-content-item",
        "https://ns.adobe.com/personalization/redirect-item",
        "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes": [
        "alloyStore",
        "siteWide",
        "__view__",
        "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
      ],
      "surfaces": [
        "web://mywebpage.html/",
        "web://mywebpage.html/#sample-json-content"
      ]
    }
  }
}
```



| Attributo | Tipo | Obbligatorio/facoltativo | Descrizione |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Obbligatorio per la personalizzazione Target. Facoltativo, ad Offer decisioning. | Elenco degli schemi utilizzati nella decisione, per selezionare il tipo di offerte restituite. |
| `scopes` | `String[]` | Facoltativo | Elenco degli ambiti decisionali. Massimo 30 per richiesta. |

## Oggetto handle {#handle}

Il contenuto personalizzato recuperato dalle soluzioni di personalizzazione viene presentato in un handle `personalization:decisions`, con il seguente formato per il payload:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Attributo | Tipo | Descrizione |
| --- | --- | --- |
| `payload.id` | Stringa | ID della decisione. |
| `payload.scope` | Stringa | Ambito della decisione che ha portato alle offerte proposte. |
| `payload.scopeDetails.decisionProvider` | Stringa | Impostato su `TGT` quando si utilizza Adobe Target. |
| `payload.scopeDetails.activity.id` | Stringa | ID univoco dell’attività di offerta. |
| `payload.scopeDetails.experience.id` | Stringa | ID univoco del posizionamento dell’offerta. |
| `items[].id` | Stringa | ID univoco del posizionamento dell’offerta. |
| `items[].data.id` | Stringa | ID dell’offerta proposta. |
| `items[].data.schema` | Stringa | Schema del contenuto associato all’offerta proposta. |
| `items[].data.format` | Stringa | Il formato del contenuto associato all’offerta proposta. |
| `items[].data.language` | Stringa | Un array di lingue associate al contenuto dell’offerta proposta. |
| `items[].data.content` | Stringa | Contenuto associato all’offerta proposta sotto forma di stringa. |
| `items[].data.selector` | Stringa | Selettore HTML utilizzato per identificare l’elemento DOM di destinazione per un’offerta di azione DOM. |
| `items[].data.prehidingSelector` | Stringa | Selettore HTML utilizzato per identificare l’elemento DOM da nascondere durante la gestione di un’offerta di azione DOM. |
| `items[].data.deliveryUrl` | Stringa | Contenuto immagine associato all’offerta proposta sotto forma di URL. |
| `items[].data.characteristics` | Stringa | Caratteristiche associate all’offerta proposta nel formato di un oggetto JSON. |

## Chiamata API di esempio {#sample-call}

**Formato API**

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
   "event":{
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
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `configId` | Stringa | Sì | ID dello stream di dati. |
| `requestId` | Stringa | No | Specifica un ID di traccia della richiesta esterno. Se non viene fornito alcun elemento, l’Edge Network ne genererà uno per te e lo restituirà nel corpo/nelle intestazioni della risposta. |

### Risposta {#response}

Restituisce uno stato `200 OK` e uno o più oggetti `Handle`, a seconda dei servizi edge abilitati nella configurazione dello stream di dati.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Notifiche {#notifications}

Le notifiche devono essere attivate quando un contenuto o una visualizzazione preacquisiti viene visitato o renderizzato all’utente finale. Affinché le notifiche vengano disattivate per l&#39;ambito corretto, assicurati di tenere traccia di `id` corrispondente per ogni ambito.

Le notifiche con il diritto `id` per gli ambiti corrispondenti devono essere attivate affinché il reporting venga rispecchiato correttamente.

**Formato API**

```http
POST /ee/v2/collect
```

### Richiesta {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
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
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sì | ID dello stream di dati utilizzato dall’endpoint di raccolta dati. |
| `requestId` | `String` | No | ID di traccia della richiesta esterna. Se non viene fornito alcun elemento, l’Edge Network ne genererà uno per te e lo restituirà nel corpo/nelle intestazioni della risposta. |
| `silent` | `Boolean` | No | Parametro booleano facoltativo che indica se l&#39;Edge Network deve restituire una risposta `204 No Content` con un payload vuoto. Gli errori critici vengono segnalati utilizzando il codice di stato HTTP e il payload corrispondenti. |

### Risposta {#notifications-response}

In caso di esito positivo, la risposta restituisce uno dei seguenti stati e `requestID`, se non ne è stato fornito alcuno nella richiesta.

* `202 Accepted` quando la richiesta è stata elaborata correttamente;
* `204 No Content` quando la richiesta è stata elaborata correttamente e il parametro `silent` è stato impostato su `true`;
* `400 Bad Request` quando la richiesta non era formata correttamente (ad esempio, l&#39;identità primaria obbligatoria non è stata trovata).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
