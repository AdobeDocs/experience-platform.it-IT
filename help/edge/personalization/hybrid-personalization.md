---
title: Personalizzazione ibrida tramite Web SDK e API del server di rete Edge
description: Questo articolo illustra come utilizzare l’SDK per web in combinazione con l’API server per distribuire la personalizzazione ibrida sulle proprietà web.
keywords: personalizzazione; ibrida; api server; lato server; implementazione ibrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# Personalizzazione ibrida tramite Web SDK e API del server di rete Edge

## Panoramica {#overview}

La personalizzazione ibrida descrive il processo di recupero dei contenuti di personalizzazione lato server, utilizzando [API server di rete Edge](../..//server-api/overview.md)e il rendering lato client, utilizzando [SDK per web](../home.md).

Puoi utilizzare la personalizzazione ibrida con soluzioni di personalizzazione come Adobe Target o Offer Decisioning. La differenza sta nei contenuti di [!UICONTROL API server] payload.

## Prerequisiti {#prerequisites}

Prima di implementare la personalizzazione ibrida nelle proprietà web, assicurati di soddisfare le seguenti condizioni:

* Hai deciso quale soluzione di personalizzazione desideri utilizzare. Questo avrà un impatto sul contenuto [!UICONTROL API server] payload.
* Si dispone dell&#39;accesso a un server applicazioni che è possibile utilizzare per [!UICONTROL API server] chiamate.
* Accesso al [API server di rete Edge](../../server-api/authentication.md).
* Hai correttamente [configurato e distribuito](../fundamentals/configuring-the-sdk.md) Web SDK sulle pagine che desideri personalizzare.

## Diagramma di flusso {#flow-diagram}

Il diagramma di flusso seguente descrive l’ordine dei passaggi effettuati per distribuire la personalizzazione ibrida.

![Diagramma di flusso visivo che mostra l’ordine dei passaggi effettuati per distribuire la personalizzazione ibrida.](assets/hybrid-personalization-diagram.png)

1. Eventuali cookie esistenti memorizzati in precedenza dal browser, con prefisso `kndctr_`, sono inclusi nella richiesta del browser.
1. Il browser Web client richiede la pagina Web dal server applicazioni.
1. Quando il server applicazioni riceve la richiesta di pagina, effettua una `POST` richiesta al [Endpoint di raccolta dati interattivi API server](../../server-api/interactive-data-collection.md) per recuperare il contenuto di personalizzazione. Il `POST` la richiesta contiene un `event` e un `query`. I cookie del passaggio precedente, se disponibili, sono inclusi nel `meta>state>entries` array.
1. L’API server restituisce il contenuto di personalizzazione al server applicazioni.
1. Il server applicazioni restituisce una risposta HTML al browser client, contenente [cookie di identità e cluster](#cookies).
1. Nella pagina del client, il [!DNL Web SDK] `applyResponse` viene chiamato il comando, passando nelle intestazioni e nel corpo del [!UICONTROL API server] risposta dal passaggio precedente.
1. Il [!DNL Web SDK] esegue il rendering del caricamento della pagina [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) offerte automaticamente, perché il `renderDecisions` il flag è impostato su `true`.
1. Basato su modulo [!DNL JSON] le offerte vengono applicate manualmente tramite `applyPersonalization` per aggiornare [!DNL DOM] in base all’offerta di personalizzazione.
1. Per le attività basate su moduli, gli eventi di visualizzazione devono essere inviati manualmente, per indicare quando è stata visualizzata l’offerta. Questa operazione viene eseguita tramite `sendEvent` comando.

## Cookie {#cookies}

I cookie vengono utilizzati per rendere persistenti l’identità dell’utente e le informazioni sul cluster.  Quando si utilizza un’implementazione ibrida, il server applicazioni Web gestisce l’archiviazione e l’invio di questi cookie durante il ciclo di vita della richiesta.

| Cookie | Finalità | Archiviato da | Inviato da |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contiene i dettagli dell’identità utente. | Server dell’applicazione | Server dell’applicazione |
| `kndctr_AdobeOrg_cluster` | Indica quale cluster di rete Edge deve essere utilizzato per soddisfare le richieste. | Server dell’applicazione | Server dell’applicazione |

## Posizionamento della richiesta {#request-placement}

Le richieste API server sono necessarie per ottenere proposte e inviare una notifica di visualizzazione. Quando si utilizza un’implementazione ibrida, il server applicazioni invia queste richieste all’API server.

| Richiesta | Creato da |
|---|---|
| Richiesta di interazione per recuperare le proposte | Server dell’applicazione |
| Richiesta di interazione per inviare notifiche di visualizzazione | Server dell’applicazione |

## implicazioni di Analytics {#analytics}

Quando implementi la personalizzazione ibrida, devi prestare particolare attenzione in modo che gli hit pagina non vengano conteggiati più volte in Analytics.

Quando [configurare uno stream di dati](../datastreams/overview.md) con Analytics, gli eventi vengono inoltrati automaticamente in modo che gli hit pagina vengano acquisiti.

Il campione di questa implementazione utilizza due diversi flussi di dati:

* Un flusso di dati configurato per Analytics. Questo flusso di dati viene utilizzato per le interazioni Web SDK.
* Un secondo stream di dati senza una configurazione Analytics. Questo flusso di dati viene utilizzato per le richieste API server.

In questo modo, la richiesta lato server non registra alcun evento Analytics, ma le richieste lato client. Questo fa sì che le richieste di Analytics vengano conteggiate con precisione.


## Richiesta lato server {#server-side-request}

La richiesta di esempio seguente illustra una richiesta API server che il server applicazioni potrebbe utilizzare per recuperare il contenuto di personalizzazione.

>[!IMPORTANT]
>
>Questa richiesta utilizza Adobe Target come soluzione di personalizzazione. La richiesta potrebbe variare in base alla soluzione di personalizzazione scelta.


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
| `dataStreamId` | `String` | Sì. | ID dello stream di dati utilizzato per passare le interazioni alla rete Edge. Consulta la [panoramica sugli stream di dati](../datastreams/overview.md) per scoprire come configurare un flusso di dati. |
| `requestId` | `String` | No | Un ID casuale per correlare le richieste interne del server. Se non ne viene fornito alcuno, la rete Edge ne genererà uno e lo restituirà nella risposta. |

### Risposta lato server {#server-response}

La risposta di esempio seguente mostra l’aspetto che potrebbe avere la risposta dell’API server.


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

Nella pagina del client, il [!DNL Web SDK] `applyResponse` viene chiamato il comando, passando nelle intestazioni e nel corpo della risposta lato server.

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

Basato su modulo [!DNL JSON] le offerte vengono applicate manualmente tramite `applyPersonalization` per aggiornare [!DNL DOM] in base all’offerta di personalizzazione. Per le attività basate su moduli, gli eventi di visualizzazione devono essere inviati manualmente, per indicare quando è stata visualizzata l’offerta. Questa operazione viene eseguita tramite `sendEvent` comando.

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

Per aiutarti a sperimentare e saperne di più su questo tipo di personalizzazione, forniamo un’applicazione di esempio che puoi scaricare e utilizzare per i test. Puoi scaricare l’applicazione, insieme a istruzioni dettagliate su come utilizzarla, da questo [Archivio GitHub](https://github.com/adobe/alloy-samples).
