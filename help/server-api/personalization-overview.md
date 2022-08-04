---
title: Panoramica sulla personalizzazione
description: Scopri come utilizzare l’API di Adobe Experience Platform Edge Network Server per recuperare contenuti personalizzati dalle soluzioni di personalizzazione Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: f36892103b0b202550c07a70538c97b1cc673840
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 9%

---

# Panoramica sulla personalizzazione

Con la [!DNL Server API], puoi recuperare contenuti personalizzati dalle soluzioni di personalizzazione Adobe, tra cui [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) e [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

Inoltre, la [!DNL Server API] potenzia le funzionalità di personalizzazione della pagina e della pagina successiva tramite destinazioni di personalizzazione Adobe Experience Platform, ad esempio [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) e [connessione di personalizzazione personalizzata](../destinations/catalog/personalization/custom-personalization.md). Per scoprire come configurare un Experience Platform per la personalizzazione della stessa pagina e della pagina successiva, consulta la sezione [guida dedicata](../destinations/ui/configure-personalization-destinations.md).

Quando utilizzi l’API server, devi integrare la risposta fornita dal motore di personalizzazione con la logica utilizzata per il rendering del contenuto sul sito. A differenza di [SDK per web](../edge/home.md), [!DNL Server API] non dispone di un meccanismo per applicare automaticamente il contenuto restituito da [!DNL Adobe Target] e [!DNL Offer Decisioning].

## Terminologia {#terminology}

Prima di lavorare con le soluzioni di personalizzazione Adobe, assicurati di comprendere i seguenti concetti:

* **Offerta**: un’offerta è un messaggio di marketing a cui possono essere associate delle regole che determinano gli utenti idonei per visualizzare l’offerta.
* **Decisione**: Una decisione (precedentemente nota come attività di offerta) informa la selezione di un’offerta.
* **Schema**: Lo schema di una decisione informa il tipo di offerta restituita.
* **Ambito**: Il campo di applicazione della decisione.
   * In Adobe Target, è la [!DNL mbox]. La [!DNL global mbox] è `__view__` scope
   * Per [!DNL Offer Decisioning], sono le stringhe JSON codificate in Base64 contenenti gli ID attività e di posizionamento che desideri che il servizio offer decisioning utilizzi per proporre offerte.

## La `query` oggetto {#query-object}

Il recupero del contenuto personalizzato richiede un oggetto query di richiesta esplicito per un esempio di richiesta. L&#39;oggetto query ha il formato seguente:

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| Attributo | Tipo | Obbligatorio/facoltativo | Descrizione |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Richiesto per la personalizzazione Target. Facoltativo, ad Offer decisioning. | Elenco degli schemi utilizzati nella decisione, per selezionare il tipo di offerte restituite. |
| `scopes` | `String[]` | Facoltativo | Elenco degli ambiti decisionali. Massimo 30 per richiesta. |

## Oggetto handle {#handle}

Il contenuto personalizzato recuperato dalle soluzioni di personalizzazione viene presentato in un `personalization:decisions` handle, con il seguente formato per il payload:

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
| `payload.id` | Stringa | ID decisione. |
| `payload.scope` | Stringa | Il campo di applicazione della decisione che ha dato luogo alle offerte proposte. |
| `payload.scopeDetails.decisionProvider` | Stringa | Imposta su `TGT` quando si utilizza Adobe Target. |
| `payload.scopeDetails.activity.id` | Stringa | ID univoco dell’attività di offerta. |
| `payload.scopeDetails.experience.id` | Stringa | ID univoco del posizionamento dell’offerta. |
| `items[].id` | Stringa | ID univoco del posizionamento dell’offerta. |
| `items[].data.id` | Stringa | ID dell’offerta proposta. |
| `items[].data.schema` | Stringa | Schema del contenuto associato all’offerta proposta. |
| `items[].data.format` | Stringa | Formato del contenuto associato all’offerta proposta. |
| `items[].data.language` | Stringa | Matrice di lingue associate al contenuto dell’offerta proposta. |
| `items[].data.content` | Stringa | Contenuto associato all’offerta proposta nel formato di una stringa. |
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
| `configId` | Stringa | Sì | ID del datastream. |
| `requestId` | Stringa | No | Fornisci un ID di traccia della richiesta esterna. Se non ne viene fornito nessuno, la rete Edge ne genererà uno per te e lo restituirà nel corpo o nelle intestazioni di risposta. |

### Risposta {#response}

Restituisce un valore `200 OK` stato e uno o più `Handle` a seconda dei servizi edge abilitati nella configurazione del datastream.

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

Le notifiche devono essere attivate quando un contenuto o una visualizzazione precaricata è stata visitata o sottoposta a rendering per l’utente finale. Per disattivare le notifiche per l’ambito corretto, assicurati di tenere traccia delle `id` per ogni ambito.

Notifiche a destra `id` affinché gli ambiti corrispondenti vengano rispecchiati correttamente, è necessario attivare gli ambiti corrispondenti.

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
| `dataStreamId` | `String` | Sì | ID del datastream utilizzato dall&#39;endpoint di raccolta dati. |
| `requestId` | `String` | No | ID traccia richiesta esterna esterna. Se non ne viene fornito nessuno, la rete Edge ne genererà uno per te e lo restituirà nel corpo o nelle intestazioni di risposta. |
| `silent` | `Boolean` | No | Parametro booleano facoltativo che indica se la rete Edge deve restituire un `204 No Content` risposta con payload vuoto. Gli errori critici vengono segnalati utilizzando il codice di stato HTTP e il payload corrispondenti. |

### Risposta {#notifications-response}

Una risposta corretta restituisce uno degli stati seguenti e un `requestID` se non ne è stato fornito nessuno nella richiesta.

* `202 Accepted` quando la richiesta è stata elaborata con successo;
* `204 No Content` quando la richiesta è stata elaborata correttamente e il `silent` è stato impostato su `true`;
* `400 Bad Request` quando la richiesta non è stata formata correttamente (ad esempio, l’identità principale obbligatoria non è stata trovata).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
