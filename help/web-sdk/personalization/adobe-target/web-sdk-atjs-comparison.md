---
title: Confronto di at.js con Experience Platform Web SDK
description: Scopri le caratteristiche di at.js rispetto a Experience Platform Web SDK
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;Decisions;scope;schema;diagramma di sistema;diagramma
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: ca1574f3f95840fce246fb4ed8845583fa0ff093
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 2%

---

# Confronto della libreria at.js con Web SDK

## Panoramica

Questo articolo fornisce una panoramica delle differenze tra la libreria `at.js` e Experience Platform Web SDK.

## Installazione delle librerie

### Installazione di at.js

Consentiamo ai nostri clienti di scaricare la libreria direttamente da Adobe Experience Cloud, nella scheda Implementazione. La libreria at.js è personalizzata con impostazioni simili a quelle del cliente: clientCode, imsOrgId, ecc.

### Installazione di Web SDK

La versione predefinita è disponibile su una rete CDN. Puoi fare riferimento alla libreria sulla rete CDN direttamente sulla tua pagina, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e non minimizzati. La versione non minimizzata è utile a scopo di debug.

Per ulteriori informazioni, vedere [Installare Web SDK utilizzando la libreria JavaScript](/help/web-sdk/install/library.md).

## Configurazione delle librerie

### Configurazione di at.js

Alla fine di ogni file at.js, troverai una sezione in cui creiamo un’istanza e trasmettiamo un oggetto impostazione. È personalizzabile, al momento del download viene compilata tale sezione con le impostazioni correnti del cliente.

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)


### Configurazione del Web SDK

La configurazione per l&#39;SDK viene eseguita con il comando [`configure`](/help/web-sdk/commands/configure/overview.md). Il comando `configure` è *always* chiamato per primo.

## Come richiedere ed eseguire il rendering automatico delle offerte di Page Load Target

### Utilizzo di at.js

Utilizzando at.js 2.x, se abiliti l&#39;impostazione `pageLoadEnabled`, la libreria attiverà una chiamata ad Edge di Target con `execute -> pageLoad`. Se tutte le impostazioni sono impostate sui valori predefiniti, non è necessaria alcuna codifica personalizzata. Una volta che at.js viene aggiunto alla pagina e caricato dal browser, viene eseguita una chiamata Edge di Target.

### Utilizzo di Web SDK

I contenuti creati nel [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) di Adobe Target possono essere recuperati e renderizzati automaticamente dall&#39;SDK.

Per richiedere ed eseguire automaticamente il rendering delle offerte di Target, utilizzare il comando `sendEvent` e impostare l&#39;opzione `renderDecisions` su `true`. In questo modo l’SDK deve eseguire automaticamente il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico.

Esempio:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Experience Platform Web SDK invia automaticamente una notifica con le offerte eseguite dall’SDK WEB. Di seguito è riportato un esempio di payload per una richiesta di notifica:

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[Ulteriori informazioni](../rendering-personalization-content.md)

## Come richiedere e NON eseguire automaticamente il rendering delle offerte di Page Load Target

### Utilizzo di at.js

Esistono due modi per attivare una chiamata a Target Edge per recuperare le offerte per il caricamento della pagina.

Esempio 1:

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

Esempio 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)

### Utilizzo di Web SDK

Eseguire un comando `sendEvent` con un ambito speciale in `decisionScopes`: `__view__`. Questo ambito viene utilizzato come segnale per recuperare tutte le attività di caricamento della pagina da Target e preacquisire tutte le visualizzazioni. L’SDK per web tenterà inoltre di valutare tutte le attività basate sulla visualizzazione del Compositore esperienza visivo. La disattivazione del preacquisizione delle visualizzazioni non è attualmente supportata in Web SDK.

Per accedere a qualsiasi contenuto di personalizzazione, puoi fornire una funzione di callback che verrà chiamata dopo che l’SDK avrà ricevuto una risposta corretta dal server. Al callback viene fornito un oggetto risultato, che può contenere una proprietà proposition contenente eventuali contenuti di personalizzazione restituiti.

Esempio:

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[Ulteriori informazioni](../rendering-personalization-content.md#manually-rendering-content)


## Richiedere mbox di Target basate su moduli specifiche


### Utilizzo di at.js

È possibile recuperare le attività del Compositore basato su moduli utilizzando la funzione `getOffer`:

Esempio 1:

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

Esempio 2:

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)


### Utilizzo di Web SDK

È possibile recuperare le attività basate su Compositore basato su moduli utilizzando il comando `sendEvent` e passando i nomi mbox sotto l&#39;opzione `decisionScopes`. Il comando `sendEvent` restituirà una promessa risolta con un oggetto contenente le attività/proposte richieste:
L&#39;array `propositions` si presenta così:

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Esempio:

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[Ulteriori informazioni](../rendering-personalization-content.md#manually-rendering-content)

## Applicare le attività Target

### Utilizzo di at.js

È possibile applicare le attività di Target utilizzando la funzione `applyOffers`: `adobe.target.applyOffer(options)`

Esempio:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

Ulteriori informazioni sul comando `applyOffers` sono disponibili nella [documentazione dedicata](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html).


### Utilizzo di Web SDK

È possibile applicare le attività di Target utilizzando il comando `applyPropositions`.

Esempio:

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

Ulteriori informazioni sul comando `applyPropositions` sono disponibili nella [documentazione dedicata](../../personalization/rendering-personalization-content.md#applypropositions).

## Come tenere traccia degli eventi

### Utilizzo di at.js

È possibile tenere traccia degli eventi utilizzando la funzione `trackEvent` o utilizzando `sendNotifications`.

Questa funzione genera una richiesta per segnalare le azioni dell’utente, ad esempio clic e conversioni. Non fornisce attività nella risposta.


**Esempio 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**Esempio 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### Utilizzo di Web SDK

È possibile tenere traccia degli eventi e delle azioni dell&#39;utente chiamando il comando `sendEvent`, popolando il gruppo di campi XDM `_experience.decisioning.propositions` e impostando `eventType` su uno dei 2 valori:

* `decisioning.propositionDisplay`: segnala il rendering dell&#39;attività Target.
* `decisioning.propositionInteract`: segnala un&#39;interazione dell&#39;utente con l&#39;attività, come un clic del mouse.

Il gruppo di campi XDM `_experience.decisioning.propositions` è un array di oggetti. Le proprietà di ciascun oggetto sono derivate da `result.propositions` restituito nel comando `sendEvent`: `{ id, scope, scopeDetails }`

**Esempio 1 - Traccia un evento `decisioning.propositionDisplay` dopo il rendering di un&#39;attività**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```

**Esempio 2 - Traccia un evento `decisioning.propositionInteract` dopo che si è verificata una metrica di clic**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[Ulteriori informazioni](../rendering-personalization-content.md#manually-rendering-content)

**Esempio 3 - Tracciare un evento generato dopo l&#39;esecuzione di un&#39;azione**

Questo esempio tiene traccia di un evento che è stato attivato dopo l’esecuzione di un’azione specifica, ad esempio il clic su un pulsante.
È possibile aggiungere altri parametri personalizzati tramite l&#39;oggetto dati `__adobe.target`.

```js
//replicates an at.js trackEvent call
alloy("sendEvent", {
    "type": "decisioning.propositionDisplay",
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "sumbitButtonClick" // Or any mbox/location name you want to use in Adobe Target
                }]
            }
        }
    }
});
```

## Come attivare una modifica della visualizzazione in un&#39;applicazione a pagina singola

### Utilizzo di at.js

Utilizzare la funzione `adobe.target.triggerView`. Questa funzione può essere chiamata ogni volta che viene caricata una nuova pagina o quando viene eseguito nuovamente il rendering di un componente di una pagina. È necessario implementare adobe.target.triggerView() per le applicazioni a pagina singola (SPA) per utilizzare il Compositore esperienza visiva per creare test A/B e attività di targeting delle esperienze (XT). Se adobe.target.triggerView() non è implementato sul sito, non è possibile utilizzare il Compositore esperienza visivo per l’SPA.

**Esempio**

```javascript
adobe.target.triggerView("homeView")
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html)


### Utilizzo di Web SDK

Per attivare o segnalare una modifica della visualizzazione di un&#39;applicazione a pagina singola, impostare la proprietà `web.webPageDetails.viewName` nell&#39;opzione `xdm` del comando `sendEvent`. Web SDK controllerà la cache di visualizzazione. Se sono presenti offerte per `viewName` specificate in `sendEvent`, verranno eseguite e verrà inviato un evento di notifica di visualizzazione.

**Esempio**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[Ulteriori informazioni](./spa-implementation.md#implementing-xdm-views)

## Come sfruttare i token di risposta

Il contenuto Personalization restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), ovvero dettagli su attività, offerta, esperienza, profilo utente, informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

### Utilizzo di at.js

Utilizza gli eventi personalizzati di at.js per ascoltare la risposta di Target e leggere i token di risposta.

**Esempio**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)


### Utilizzo di Web SDK

>[!IMPORTANT]
>
>Assicurati di utilizzare Platform Web SDK versione 2.6.0 o successiva.

I token di risposta vengono restituiti come parte di `propositions` esposti nel risultato del comando `sendEvent`. Ogni proposta contiene un array di `items` e ogni elemento avrà un oggetto `meta` compilato con i token di risposta se sono abilitati nell&#39;interfaccia utente di amministrazione di Target. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

**Esempio**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[Ulteriori informazioni](./accessing-response-tokens.md)

## Come gestire la visualizzazione momentanea di altri contenuti

### Utilizzo di at.js

Utilizzando at.js puoi gestire la visualizzazione momentanea di altri contenuti impostando `bodyHidingEnabled: true` in modo che at.js si occupi di
nascondere anticipatamente i contenitori personalizzati prima che vengano recuperate e applicate le modifiche DOM.
Le sezioni di pagina che contengono contenuto personalizzato possono essere pre-nascoste eseguendo l&#39;override di at.js `bodyHiddenStyle`.
Per impostazione predefinita `bodyHiddenStyle` nasconde l&#39;intero HTML `body`.
Entrambe le impostazioni possono essere ignorate utilizzando `window.targetGlobalSettings`. È necessario inserire `window.targetGlobalSettings` prima di caricare at.js.

### Utilizzo di Web SDK

Utilizzando Web SDK, il cliente può impostare il proprio stile di pre-hiding nel comando di configurazione, come nell’esempio seguente:

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Quando si carica l’SDK Web in modalità asincrona, si consiglia di inserire il seguente snippet nella pagina prima di inserire l’SDK Web:

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## Come viene gestito A4T

### Utilizzo di at.js

Esistono 2 tipi di registrazione A4T supportati utilizzando at.js:

* Registrazione lato client di Analytics
* Registrazione lato server di Analytics

#### Registrazione lato client di Analytics

**Esempio 1: utilizzo dell&#39;impostazione globale di Target**

La registrazione lato client di Analytics può essere abilitata impostando `analyticsLogging: client_side` nelle impostazioni at.js o ignorando l&#39;oggetto `window.targetglobalSettings`.
Quando questa opzione è impostata, il formato del payload restituito è simile al seguente:

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

Il payload può quindi essere inoltrato ad Analytics tramite l’API di inserimento dati.

Esempio 2: configurazione in ogni funzione `getOffers`:

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

Ecco come si presenta il payload di risposta:

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Il payload di Analytics (`tnta` token) deve essere incluso nell&#39;hit di Analytics utilizzando [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

#### Registrazione lato server di Analytics

La registrazione lato server di Analytics può essere abilitata impostando `analyticsLogging: server_side` nelle impostazioni at.js o ignorando l&#39;oggetto `window.targetglobalSettings`.
I dati scorrono quindi come segue:

![Diagramma che mostra il flusso di lavoro di registrazione lato server di Analytics](assets/a4t-server-side-atjs.png)

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### Utilizzo di Web SDK

L’SDK per web supporta anche:

* Registrazione lato client di Analytics
* Registrazione lato server di Analytics

#### Registrazione lato client di Analytics

La funzione di registrazione lato client di Analytics è abilitata quando Adobe Analytics è disabilitata per tale configurazione di DataStream.

![Diagramma che mostra il flusso di lavoro di registrazione lato client di Analytics](assets/analytics-disabled-datastream-config.png)

Il cliente ha accesso al token di Analytics (`tnta`) che deve essere condiviso con Analytics tramite [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
in concatenando il comando `sendEvent` e scorrendo l&#39;array di proposizioni risultante.

**Esempio**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

Ecco un diagramma per mostrare il flusso dei dati quando è abilitato Analytics Client Side:

![Diagramma del flusso dei dati nella registrazione lato client di Analytics](assets/analytics-client-side-logging.png)

#### Registrazione lato server di Analytics

La funzione di registrazione lato server di Analytics è abilitata quando Analytics è abilitata per tale configurazione di DataStream.

![Interfaccia utente per gli stream di dati con le impostazioni di Analytics.](assets/analytics-enabled-datastream-config.png)

Quando la funzione di registrazione Analytics lato server è abilitata, il payload A4T che deve essere condiviso con Analytics in modo che il reporting di Analytics mostri
le impression e le conversioni corrette vengono condivise a livello di Edge Network, in modo che il cliente non debba eseguire alcuna elaborazione aggiuntiva.

Ecco come fluiscono i dati nei nostri sistemi quando è abilitata la registrazione di Analytics lato server:

![Diagramma che mostra il flusso di dati nella registrazione di Analytics lato server](assets/analytics-server-side-logging.png)

## Come impostare le impostazioni globali di Target

### Utilizzo di at.js

È possibile modificare le impostazioni nella libreria at.js utilizzando `window.targetGlobalSettings`, anziché configurare le impostazioni nell&#39;interfaccia utente di Target Standard/Premium o utilizzando le API REST.

La sostituzione deve essere definita prima che at.js sia caricato o in Amministrazione > Implementazione > Modifica impostazioni at.js > Impostazioni codice > Intestazione libreria.

Esempio:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### Utilizzo di Web SDK

Questa funzione non è supportata in Web SDK.

## Come aggiornare gli attributi del profilo di Target

### Utilizzo di at.js

**Esempio 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**Esempio 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### Utilizzo di Web SDK

Per aggiornare un profilo di Target, utilizzare il comando `sendEvent` e impostare la proprietà `data.__adobe.target`, prefissando i nomi delle chiavi mediante `profile`.

**Esempio**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Come si utilizza Target Recommendations

### Utilizzo di at.js

**Esempio 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**Esempio 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)


### Utilizzo di Web SDK

Per inviare i dati dei consigli, utilizzare il comando `sendEvent` e impostare la proprietà `data.__adobe.target`, prefissando i nomi delle chiavi con il prefisso `entity`.

**Esempio**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## Come si utilizzano gli ID di terze parti

### Utilizzo di at.js

Utilizzando at.js è possibile inviare `mbox3rdPartyId` in diversi modi, utilizzando `getOffer` o `getOffers`:

**Esempio 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**Esempio 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

In alternativa, è possibile impostare `mbox3rdPartyId` in `targetPageParams` o `targetPageParamsAll`.
Quando viene impostato in `targetPageParams`, verrà inviato nelle richieste per `target-global-mbox` note anche come `pag-lLoad`.
Il consiglio deve essere impostato utilizzando `targetPageParamsAll` poiché verrà inviato in ogni richiesta di destinazione.
Il vantaggio dell&#39;utilizzo di `targetPageParamsAll` è che è possibile definire `mbox3rdPartyId` sulla pagina una sola volta e questo assicurerà che tutte le richieste di destinazione abbiano il diritto `mbox3rdPartyId`.

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### Utilizzo di Web SDK

SDK per web supporta l’ID di terze parti di Target. Tuttavia, richiede alcuni passaggi aggiuntivi. Prima di iniziare a utilizzare la soluzione, è necessario parlare di `identityMap`.
Identity Map consente ai clienti di inviare più identità. Tutte le identità sono namespace. Ogni spazio dei nomi può avere una o più identità. Una particolare identità può essere contrassegnata come primaria.
Tenendo conto di queste informazioni, possiamo vedere quali sono i passaggi necessari per impostare l’SDK web per utilizzare l’ID di terze parti di Target.

1. Imposta lo spazio dei nomi che conterrà l’ID di terze parti di Target nella pagina di configurazione dello stream di dati:

![Interfaccia utente Datastreams con il campo spazio dei nomi dell&#39;ID di terze parti di Target](assets/mbox-3-party-id-setup.png)

1. Invia lo spazio dei nomi dell’identità in ogni comando sendEvent come segue:

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## Come si impostano i token di proprietà

### Utilizzo di at.js

Con at.js è possibile impostare i token di proprietà in due modi, utilizzando `targetPageParams` o `targetPageParamsAll`. Con `targetPageParams` il token di proprietà viene aggiunto alla chiamata `target-global-mbox`, ma con `targetPageParamsAll` il token viene aggiunto a tutte le chiamate di destinazione:

**Esempio 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**Esempio 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### Utilizzo di Web SDK

Utilizzando Web SDK, i clienti possono impostare la proprietà a un livello più alto, durante la configurazione del flusso di dati, in Adobe Target namespace:
![Interfaccia utente per gli stream di dati con le impostazioni di Adobe Target.](assets/at-property-setup.png)
Ciò significa che ogni chiamata di Target per quella specifica configurazione di Flusso di dati conterrà quel token di proprietà.

## Come posso preacquisire gli elementi mbox

### Utilizzo di at.js

Questa funzionalità è disponibile solo in at.js 2.x. In at.js 2.x è presente una nuova funzione denominata `getOffers`. `getOffers` consente ai clienti di preacquisire il contenuto per una o più mbox. Ecco un esempio:

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

NOTA: si consiglia di verificare che ogni `mbox` nell&#39;array `mboxes` abbia il proprio indice. Di solito la prima mbox ha `index=0`, la successiva `index=1`, ecc.

### Utilizzo di Web SDK

Questa funzionalità non è attualmente supportata in Web SDK.

## Come si esegue il debug dell’implementazione di Target

### Utilizzo di at.js

At.js espone le seguenti funzioni di debug:

* Mbox Disable (Disabilita mbox): disabilita il recupero e il rendering di Target per verificare se la pagina è interrotta senza le interazioni di Target
* Debug mbox: at.js registra ogni azione
* Traccia di destinazione: con un token di traccia mbox generato in Bullseye, un oggetto di traccia con i dettagli che hanno partecipato al processo decisionale è disponibile nell&#39;oggetto `window.___target_trace`

Nota: tutte queste funzionalità di debug sono disponibili con funzionalità avanzate in [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Utilizzo di Web SDK

Sono disponibili più funzionalità di debug quando si utilizza Web SDK:

* Utilizzo di [Assurance](/help/assurance/home.md)
* [Debug di Web SDK abilitato](/help/web-sdk/use-cases/debugging.md)
* Usa [hook di monitoraggio SDK Web](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Usa [Adobe Experience Platform Debugger](/help/debugger/home.md)
* Traccia di destinazione
