---
title: Personalization tramite Adobe Target
description: Scopri come utilizzare l’API server per distribuire ed eseguire il rendering di esperienze personalizzate create in Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Personalization tramite Adobe Target

## Panoramica {#overview}

L&#39;API server Edge Network può distribuire ed eseguire il rendering di esperienze personalizzate create in Adobe Target, con l&#39;aiuto del [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

>[!IMPORTANT]
>
>Le esperienze Personalization create tramite il Compositore esperienza visivo di [Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) non sono completamente supportate dall&#39;API server. L&#39;API server può **recuperare** attività create dal Compositore esperienza visivo, ma l&#39;API server non può **eseguire il rendering** delle attività create dal Compositore esperienza visivo. Se desideri eseguire il rendering delle attività create dal Compositore esperienza visivo, implementa [la personalizzazione ibrida](../web-sdk/personalization/hybrid-personalization.md) utilizzando Web SDK e l&#39;API server Edge Network.

## Configurare lo stream di dati {#configure-your-datastream}

Prima di poter utilizzare l’API server in combinazione con Adobe Target, devi abilitare la personalizzazione Adobe Target nella configurazione dello stream di dati.

Per informazioni dettagliate su come abilitare Adobe Target, consulta la [guida sull&#39;aggiunta di servizi a uno stream di dati](../datastreams/overview.md#adobe-target-settings).

Durante la configurazione dello stream di dati, è possibile (facoltativamente) fornire valori per [!DNL Property Token], [!DNL Target Environment ID] e [!DNL Target Third Party ID Namespace].

![Immagine dell&#39;interfaccia utente che mostra la schermata di configurazione del servizio stream di dati, con Adobe Target selezionato](assets/target-datastream.png)

## Parametri personalizzati {#custom-parameters}

La maggior parte dei campi nella porzione [!DNL XDM] di ogni richiesta viene serializzata in notazione con punto e quindi inviata a Target come parametri personalizzati o [!DNL mbox].


### Esempio {#custom-parameters-example}

Dato il seguente esempio XDM:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Durante la creazione di tipi di pubblico in Target, i seguenti valori saranno disponibili come parametri personalizzati:

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Aggiornamenti del profilo di Target {#profile-update}

[!DNL Server API] consente aggiornamenti al profilo Target. Per aggiornare un profilo di Target, assicurarsi che i dati del profilo vengano passati nella porzione `data` della richiesta nel seguente formato:

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## Query delle attività di Target {#querying-target-activities}

### Schemi {#schemas}

La porzione della richiesta relativa alla query determina il contenuto restituito da Target. Nell&#39;oggetto `personalization`, `schemas` determina il tipo di contenuto da restituire da Target.

In situazioni in cui non sei sicuro del tipo di offerte che recupererai, devi includere tutti e quattro gli schemi nella query di personalizzazione per l’Edge Network:

* **Offerte basate su HTML:**
https://ns.adobe.com/personalization/html-content-item
* **Offerte basate su JSON:**
https://ns.adobe.com/personalization/json-content-item
* **Offerte di reindirizzamento di Target**
https://ns.adobe.com/personalization/redirect-item
* **Offerte di manipolazione DOM di Target**
https://ns.adobe.com/personalization/dom-action

### Ambiti decisionali {#decision-scopes}

I nomi di Adobe Target [!DNL mbox] devono essere inclusi nell&#39;array `decisionScopes` per restituire il contenuto appropriato.

#### Esempio {#decision-scopes-example}

Nell&#39;esempio seguente, tutti e quattro i tipi di offerta sono richiesti insieme a un&#39;attività Target denominata `serverapimbox`.

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
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

Di seguito è descritta una richiesta completa che include un oggetto XDM completo, parametri di profilo e la query di destinazione appropriata.

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
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### Risposta {#response}

L’Edge Network restituirà una risposta simile a quella riportata di seguito.

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
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
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

Se il visitatore è idoneo per un&#39;attività di personalizzazione basata sui dati inviati ad Adobe Target, il contenuto dell&#39;attività pertinente verrà trovato nell&#39;oggetto `handle`, dove il tipo è `personalization:decisions`.

A volte verranno restituiti anche altri contenuti in `handle`. Altri tipi di contenuto non sono rilevanti per la personalizzazione Target. Se il visitatore è idoneo per più attività, ogni attività sarà un oggetto `personalization` separato nell&#39;array.

La tabella seguente spiega gli elementi chiave di quella parte della risposta.

| Proprietà | Descrizione | Esempio |
|---|---|---|
| `scope` | Il nome mbox di Target che ha generato le offerte proposte. | `"scope": "serverapimbox"` |
| `items[].schema` | Schema del contenuto associato all’offerta proposta. Sarà correlato al tipo di attività selezionato durante la creazione dell’attività di personalizzazione. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | ID univoco dell’attività di offerta. In genere è un numero di 6 cifre. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Nome dell&#39;attività di offerta specificata dall&#39;utente. Questo viene fornito durante il passaggio di creazione dell’attività. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | ID univoco dell’esperienza di personalizzazione. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Nome univoco dell’esperienza di personalizzazione. | `"experience.name": "Experience A"` |
| `items[].data.id` | ID dell’offerta proposta. | `"id": "282484"` |
| `items[].data.format` | Il formato del contenuto associato all’offerta proposta. | `"format: "application/json` |
| `items[].data.content` | Contenuto associato all’offerta proposta. Verrà utilizzato per la personalizzazione del contenuto dell’applicazione chiamante. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## Applicazione di esempio per la personalizzazione lato server {#sample}

L&#39;applicazione di esempio trovata in [questo URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side) dimostra di utilizzare Adobe Experience Platform per ottenere contenuti di personalizzazione da Adobe Target. La pagina web cambia in base al contenuto di personalizzazione restituito.

In questo esempio _not_ si basa su librerie lato client come [!DNL Web SDK] per ottenere contenuti di personalizzazione. Invece, utilizza le API Adobe Experience Platform per recuperare il contenuto di personalizzazione. Quindi l’implementazione genera il lato server di HTML in base al contenuto di personalizzazione restituito.
