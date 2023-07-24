---
title: Personalizzazione tramite Offer Decisioning
description: Scopri come utilizzare l’API server per distribuire ed eseguire il rendering di esperienze personalizzate tramite Offer Decisioning.
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---

# Personalizzazione tramite Offer Decisioning

## Panoramica {#overview}

L’API del server di rete Edge può fornire esperienze personalizzate gestite in [Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) al canale web.

[!DNL Offer Decisioning] supporta un’interfaccia non visiva per creare, attivare e distribuire le attività e le esperienze di personalizzazione.

## Prerequisiti {#prerequisites}

Personalizzazione tramite [!DNL Offer Decisioning] richiede di avere accesso a [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) prima di configurare l’integrazione.

## Configurare lo stream di dati {#configure-your-datastream}

Prima di poter utilizzare l’API server in combinazione con Offer Decisioning, è necessario abilitare la personalizzazione Adobe Experience Platform nella configurazione dello stream di dati e abilitare **[!UICONTROL Offer decisioning]** opzione.

Consulta la [guida sull’aggiunta di servizi a un flusso di dati](../datastreams/overview.md#adobe-experience-platform-settings), per informazioni dettagliate su come abilitare Offer Decisioning.

![Immagine dell’interfaccia utente che mostra la schermata di configurazione del servizio di stream di dati, con Offer decisioning selezionato](assets/aep-od-datastream.png)

## Creazione di un pubblico {#audience-creation}

[!DNL Offer Decisioning] si basa sul servizio di segmentazione di Adobe Experience Platform per la creazione di tipi di pubblico. Puoi trovare la documentazione di [!DNL Segmentation Service] [qui](../segmentation/home.md).

## Definizione degli ambiti decisionali {#creating-decision-scopes}

Il [!DNL Offer Decision Engine] utilizza i dati Adobe Experience Platform e [Profili cliente in tempo reale](../profile/home.md), insieme al [!DNL Offer Library], per offrire offerte ai clienti e ai canali giusti al momento giusto.

Per ulteriori informazioni su [!DNL Offer Decisioning Engine], consulta la sezione dedicata [documentazione](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=it).

Dopo [configurazione dello stream di dati](#configure-your-datastream), devi definire gli ambiti decisionali da utilizzare nella campagna di personalizzazione.

[Ambiti decisionali](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) sono le stringhe JSON con codifica Base64 contenenti gli ID di attività e posizionamento che desideri [!DNL Offer Decisioning Service] da utilizzare per la proposta di offerte.

**JSON ambito decisione**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**Stringa con codifica Base64 dell&#39;ambito decisionale**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

Dopo aver creato le offerte e le raccolte, devi definire una [ambito della decisione](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes).

Copia l’ambito di decisione con codifica Base64. Lo utilizzerai in `query` oggetto della richiesta API server.

![Immagine dell’interfaccia utente che mostra l’interfaccia utente di Offer decisioning ed evidenzia l’ambito della decisione.](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## Esempio di chiamata API {#api-example}

**Formato API**

```http
POST /ee/v2/interact
```

### Richiesta {#request}

Di seguito è descritta una richiesta completa che include un oggetto XDM completo, un oggetto dati e una query di Offer decisioning.

>[!NOTE]
>
>Il `xdm` e `data` gli oggetti sono facoltativi e sono obbligatori solo ad Offer decisioning se sono stati creati segmenti con condizioni che utilizzano campi in uno di questi oggetti.

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
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
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            }
        },
        "data": {
            "page": {
                "pageInfo": {
                    "pageName": "Promotions",
                    "siteSection": "Home"
                },
                "promos": {
                    "heroPromos": "purse,shoes,sunglasses"
                },
                "customVariables": {
                    "testGroup": "orange/black theme"
                },
                "events": {
                    "homePage": true
                },
                "products": [
                    {
                        "productSKU": "abc123",
                        "productName": "shirt"
                    }
                ]
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### Risposta {#response}

La rete Edge restituirà una risposta simile a quella riportata di seguito.

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Se il visitatore è idoneo per un’attività di personalizzazione basata sui dati inviati a [!DNL Offer Decisioning], il contenuto pertinente dell&#39;attività si trova sotto `handle` oggetto, dove il tipo è `personalization:decisions`.

Gli altri contenuti verranno restituiti sotto `handle` oggetto. Altri tipi di contenuto non sono rilevanti per [!DNL Offer Decisioning] personalizzazione. Se il visitatore è idoneo per più attività, queste saranno contenute in un array.

La tabella seguente spiega gli elementi chiave di quella parte della risposta.

| Proprietà | Descrizione | Esempio |
|---|---|---|
| `scope` | Ambito di decisione associato alle offerte proposte restituite. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID univoco dell’attività di offerta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID univoco del posizionamento dell’offerta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID univoco dell’offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Schema del contenuto associato all’offerta proposta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID univoco dell’offerta proposta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Il formato del contenuto associato all’offerta proposta. | `"format": "text/html"` |
| `language` | Un array di lingue associate al contenuto dell’offerta proposta. | `"language": [ "en-US" ]` |
| `content` | Contenuto associato all’offerta proposta sotto forma di stringa. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenuto immagine associato all’offerta proposta sotto forma di URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Oggetto JSON contenente le caratteristiche associate all’offerta proposta. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
