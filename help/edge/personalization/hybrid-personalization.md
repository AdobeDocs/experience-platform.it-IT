---
title: Personalizzazione ibrida tramite SDK per web e API server di rete Edge
description: Questo articolo illustra come utilizzare l’SDK per web insieme all’API server per distribuire la personalizzazione ibrida sulle proprietà web.
keywords: personalizzazione; ibrido; api del server; lato server; implementazione ibrida;
source-git-commit: f280d4cbcde434ccf36df37e95f1902cfd02c96c
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---


# Personalizzazione ibrida tramite SDK per web e API server di rete Edge

## Panoramica {#overview}

La personalizzazione ibrida descrive il processo di recupero del contenuto di personalizzazione lato server tramite l’ [API server di rete Edge](../..//server-api/overview.md), e eseguirne il rendering lato client, utilizzando [SDK per web](../home.md).

Puoi utilizzare la personalizzazione ibrida con soluzioni di personalizzazione come Adobe Target o Offer Decisioning, con la differenza che i contenuti sono [!UICONTROL API server] carico utile.

## Prerequisiti {#prerequisites}

Prima di implementare la personalizzazione ibrida sulle proprietà web, assicurati di soddisfare le seguenti condizioni:

* Hai deciso quale soluzione di personalizzazione desideri utilizzare. Questo avrà un impatto sui contenuti del [!UICONTROL API server] carico utile.
* È possibile accedere a un server applicazioni che è possibile utilizzare per [!UICONTROL API server] chiamate.
* Hai accesso al [API server di rete Edge](../../server-api/authentication.md).
* Hai corretto [configurati e distribuiti](../fundamentals/configuring-the-sdk.md) SDK per web sulle pagine che desideri personalizzare.

## Diagramma di flusso {#flow-diagram}

Il diagramma di flusso seguente descrive l’ordine dei passaggi effettuati per distribuire la personalizzazione ibrida.

![Diagramma di flusso visivo che mostra l’ordine dei passaggi effettuati per distribuire la personalizzazione ibrida.](assets/hybrid-personalization-diagram.png)

1. Eventuali cookie esistenti precedentemente memorizzati dal browser, con prefisso `kndctr_`, sono inclusi nella richiesta del browser.
1. Il browser Web client richiede la pagina Web dal server applicazioni.
1. Quando l&#39;application server riceve la richiesta di pagina, effettua un `POST` richiesta al [Endpoint di raccolta dati interattivi API server](../../server-api/interactive-data-collection.md) per recuperare il contenuto della personalizzazione. La `POST` la richiesta contiene un `event` e `query`. I cookie del passaggio precedente, se disponibili, sono inclusi nella `meta>state>entries` array.
1. L’API server restituisce il contenuto di personalizzazione al server delle applicazioni.
1. Il server applicazioni restituisce una risposta HTML al browser client, contenente il [cookie di identità e cluster](#cookies).
1. Nella pagina del client, il [!DNL Web SDK] `applyResponse` viene chiamato, passando le intestazioni e il corpo del [!UICONTROL API server] risposta dal passaggio precedente.
1. La [!DNL Web SDK] esegue il rendering del caricamento della pagina [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) offre automaticamente, perché `renderDecisions` flag impostato su `true`.
1. Basato su modulo [!DNL JSON] le offerte vengono applicate manualmente tramite `applyPersonalization` per aggiornare [!DNL DOM] in base all’offerta di personalizzazione.
1. Per le attività basate su moduli, è necessario inviare manualmente gli eventi di visualizzazione per indicare quando l’offerta è stata visualizzata. Questo avviene tramite il `sendEvent` comando.

## Cookie {#cookies}

I cookie vengono utilizzati per mantenere l&#39;identità utente e le informazioni sui cluster.  Quando si utilizza un&#39;implementazione ibrida, il server dell&#39;applicazione Web gestisce la memorizzazione e l&#39;invio di questi cookie durante il ciclo di vita della richiesta.

| Cookie | Finalità | Memorizzato da | Inviato da |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contiene i dettagli dell’identità utente. | Server dell’applicazione | Server dell’applicazione |
| `kndctr_AdobeOrg_cluster` | Indica il cluster di rete Edge da utilizzare per soddisfare le richieste. | Server dell’applicazione | Server dell’applicazione |

## Inserimento di richieste {#request-placement}

Le richieste API del server sono necessarie per ottenere le proposte e inviare una notifica di visualizzazione. Quando si utilizza un&#39;implementazione ibrida, il server applicazioni effettua queste richieste all&#39;API server.

| Richiesta | Realizzato da |
|---|---|
| Richiesta di interazione per recuperare le proposte | Server dell’applicazione |
| Richiesta di interazione per inviare notifiche di visualizzazione | Server dell’applicazione |

## Implicazioni di Analytics {#analytics}

Quando implementi la personalizzazione ibrida, devi prestare particolare attenzione affinché gli hit di pagina non vengano conteggiati più volte in Analytics.

Quando [configurare un datastream](../datastreams/overview.md) per Analytics, gli eventi vengono inoltrati automaticamente in modo da acquisire gli hit di pagina.

L&#39;esempio di questa implementazione utilizza due diversi datastreams:

* Un datastream configurato per Analytics. Questo datastream viene utilizzato per le interazioni SDK per web.
* Un secondo datastream senza una configurazione Analytics. Questo datastream viene utilizzato per le richieste API del server.

In questo modo, la richiesta lato server non registra eventi di Analytics, ma le richieste lato client sì. Questo fa sì che le richieste di Analytics vengano conteggiate con precisione.


## Richiesta lato server {#server-side-request}

La richiesta di esempio riportata di seguito illustra una richiesta API server che il server applicazioni potrebbe utilizzare per recuperare il contenuto di personalizzazione.

>[!IMPORTANT]
>
>Questa richiesta di esempio utilizza Adobe Target come soluzione di personalizzazione. La richiesta può variare a seconda della soluzione di personalizzazione scelta.


**Formato API**

```http
POST /ee/v2/interact
```

### Richiesta {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Parametro | Tipo | Obbligatorio | Descrizione |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sì. | ID del datastream utilizzato per passare le interazioni alla rete Edge. Consulta la sezione [panoramica dei datastreams](../datastreams/overview.md) per scoprire come configurare un datastream. |
| `requestId` | `String` | No | Un ID casuale per le richieste server interne correlate. Se non ne viene fornito nessuno, la rete Edge ne genererà uno e lo restituirà nella risposta. |

### Risposta lato server {#server-response}

La risposta di esempio seguente mostra l&#39;aspetto della risposta API server.


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## Richiesta lato client {#client-request}

Nella pagina del client, il [!DNL Web SDK] `applyResponse` viene chiamato , passando le intestazioni e il corpo della risposta lato server.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

Basato su modulo [!DNL JSON] le offerte vengono applicate manualmente tramite `applyPersonalization` per aggiornare [!DNL DOM] in base all’offerta di personalizzazione. Per le attività basate su moduli, è necessario inviare manualmente gli eventi di visualizzazione per indicare quando l’offerta è stata visualizzata. Questo avviene tramite il `sendEvent` comando.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## Applicazione di esempio {#sample-app}

Per aiutarti a sperimentare e scoprire di più su questo tipo di personalizzazione, forniamo un’applicazione di esempio che puoi scaricare e utilizzare per i test. È possibile scaricare l&#39;applicazione, insieme a istruzioni dettagliate su come usarla, da questo [Archivio GitHub](https://github.com/adobe/alloy-samples).






