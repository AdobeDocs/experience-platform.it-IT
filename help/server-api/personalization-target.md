---
title: Personalizzazione tramite Adobe Target
description: Scopri come utilizzare l’API server per distribuire ed eseguire il rendering di esperienze personalizzate create in Adobe Target.
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: 3730a9a20644291db844ecfad88355daa4a1cba7
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 3%

---

# Personalizzazione tramite Adobe Target

## Panoramica {#overview}

Con l’aiuto di [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>Esperienze di personalizzazione create tramite [Compositore esperienza visivo di Target](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) non sono completamente supportati dall&#39;API server. L&#39;API del server può **retrieve** attività create dal Compositore esperienza visivo, ma l’API del server non può **rendering** attività create dal Compositore esperienza visivo. Se desideri eseguire il rendering delle attività create dal Compositore esperienza visivo, implementa [personalizzazione ibrida](../edge/personalization/hybrid-personalization.md) mediante l’SDK per web e l’API del server di rete Edge.

## Configurare il datastream {#configure-your-datastream}

Prima di poter utilizzare l&#39;API server insieme ad Adobe Target, devi abilitare la personalizzazione Adobe Target nella configurazione del datastream.

Consulta la sezione [guida sull’aggiunta di servizi a un datastream](../edge/datastreams/overview.md#adobe-target-settings), per informazioni dettagliate su come abilitare Adobe Target.

Durante la configurazione del datastream, puoi (facoltativamente) fornire valori per [!DNL Property Token], [!DNL Target Environment ID]e [!DNL Target Third Party ID Namespace].

![Immagine dell&#39;interfaccia utente che mostra la schermata di configurazione del servizio datastream, con Adobe Target selezionato](assets/target-datastream.png)

Puoi scegliere tra le seguenti opzioni [!DNL Analytics Logging] opzioni:

* **[!DNL Server Side]**: Questa è l’opzione predefinita per [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=it). Quando questa opzione è selezionata, ogni volta che Target restituisce il contenuto di personalizzazione, il [!DNL A4T] i dati vengono inviati automaticamente ad Analytics, in base alla risposta dal motore di personalizzazione di Target.
* **[!DNL Client Side]**: Quando questa opzione è selezionata, ogni volta che Target restituisce il contenuto di personalizzazione, il [!DNL A4T] i dati vengono restituiti all&#39;applicazione chiamante. Se desideri registrare questi dati in Analytics, assicurati che siano segnalati in una chiamata successiva a [!DNL Analytics].

   >[!IMPORTANT]
   >
   >Oltre a selezionare **[!UICONTROL Lato client]** nella configurazione di Target, devi anche disabilitare Analytics affinché la rete Edge restituisca il [!DNL A4T] le informazioni tornano alla risposta.


## Parametri personalizzati {#custom-parameters}

La maggior parte dei campi [!DNL XDM] parte di ogni richiesta viene serializzata in notazione del punto e quindi inviata a Target come personalizzata o [!DNL mbox] Parametri.


### Esempio {#custom-parameters-example}

Dato il seguente campione XDM:

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

Quando crei un pubblico in Target, i seguenti valori saranno disponibili come parametri personalizzati:

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Aggiornamenti dei profili di Target {#profile-update}

La [!DNL Server API] consente aggiornamenti al profilo di Target. Per aggiornare un profilo Target, assicurati che i dati del profilo siano trasmessi nella `data` parte della richiesta nel seguente formato:

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

La parte query della richiesta determina quale contenuto viene restituito da Target. Sotto la `personalization` oggetto, `schemas` determina il tipo di contenuto che Target deve restituire.

In situazioni in cui non sei sicuro del tipo di offerte che recupererai, dovresti includere tutti e quattro gli schemi nella query di personalizzazione su Edge Network:

* **Offerte basate su HTML:**
https://ns.adobe.com/personalization/html-content-item
* **Offerte basate su JSON:**
https://ns.adobe.com/personalization/json-content-item
* **Offerte di reindirizzamento di Target**
https://ns.adobe.com/personalization/redirect-item
* **Offerte di manipolazione DOM di Target**
https://ns.adobe.com/personalization/dom-action

### Ambiti decisionali {#decision-scopes}

Adobe Target [!DNL mbox] i nomi devono essere inclusi nella `decisionScopes` per restituire il contenuto appropriato.

#### Esempio {#decision-scopes-example}

Nell’esempio seguente, tutti e quattro i tipi di offerta sono richiesti insieme a un’attività Target denominata `serverapimbox`.

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

Di seguito è descritta una richiesta completa che include un oggetto XDM completo, parametri di profilo, insieme alla query Target appropriata.

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

La rete Edge restituirà una risposta simile a quella riportata di seguito.

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

Se il visitatore è idoneo per un’attività di personalizzazione basata sui dati inviati ad Adobe Target, il contenuto dell’attività rilevante si troverà nella sezione `handle` oggetto, dove è il tipo `personalization:decisions`.

Talvolta viene restituito altro contenuto in `handle` anche. Altri tipi di contenuto non sono rilevanti per la personalizzazione Target. Se il visitatore è idoneo per più attività, ogni attività sarà una separata `personalization` nell&#39;array.

La tabella seguente spiega gli elementi chiave di quella parte della risposta.

| Proprietà | Descrizione | Esempio |
|---|---|---|
| `scope` | Nome della mbox di Target risultante nelle offerte proposte. | `"scope": "serverapimbox"` |
| `items[].schema` | Schema del contenuto associato all’offerta proposta. Questo sarà correlato al tipo di attività selezionata al momento della creazione dell’attività di personalizzazione. | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | ID univoco dell’attività di offerta. Di solito un numero a 6 cifre. | `"activity.id": "140281"` |
| `items[].meta.activity.name` | Nome dell’attività di offerta specificata dall’utente. Questo viene fornito durante il passaggio di creazione dell’attività. | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | ID univoco dell’esperienza di personalizzazione. | `"experience.id": "0"` |
| `items[].meta.experience.name` | Nome univoco dell’esperienza di personalizzazione. | `"experience.name": "Experience A"` |
| `items[].data.id` | ID dell’offerta proposta. | `"id": "282484"` |
| `items[].data.format` | Formato del contenuto associato all’offerta proposta. | `"format: "application/json` |
| `items[].data.content` | Contenuto associato all’offerta proposta. Verrà utilizzato per la personalizzazione del contenuto dell’applicazione chiamante. | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
