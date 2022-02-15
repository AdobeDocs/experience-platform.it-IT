---
title: Confronto di at.js con l’SDK per web di Platform
description: Scopri in che modo le funzioni di at.js sono paragonabili agli SDK web
keywords: target;adobe target;activity.id;experience.id;renderdecisions;decisionScopes;pre-hiding snippet;vec;Compositore esperienza basato su moduli;xdm;tipi di pubblico;decisioni;ambito;schema;diagramma di sistema;diagramma
source-git-commit: 95c6d0d20ee04affb4b67c3d9f90d80e655e2752
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 7%

---

# Confronto della libreria at.js con l’SDK web

## Panoramica

Questo articolo fornisce una panoramica delle differenze tra i `at.js` e l&#39;SDK per web di Experience Platform.

## Installazione delle librerie

### Installazione di at.js

Consentiamo ai nostri clienti di scaricare la libreria direttamente dalla scheda Implementazione di Adobe Experience Cloud. La libreria at.js è personalizzata con impostazioni simili a quelle del cliente: clientCode, imsOrgId, ecc.

### Installazione dell’SDK per web

La versione precompilata è disponibile su una rete CDN. Puoi fare riferimento alla libreria sulla rete CDN direttamente sulla tua pagina, oppure scaricarla e ospitarla sulla tua infrastruttura. È disponibile in formati minimizzati e non minimizzati. La versione non minimizzata è utile a scopo di debug.

Struttura URL: https://cdn1.adoberesources.net/alloy/[VERSIONE]/alloy.min.js OR alloy.js per la versione non minimizzata.

Esempio:

* Minimizzato: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js)
* Non minimizzato: [https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js](https://cdn1.adoberesources.net/alloy/2.6.4/alloy.js)

[Per saperne di più](../../fundamentals/installing-the-sdk.md)

## Configurazione delle librerie

### Configurazione di at.js

Alla fine di ogni file at.js, troverai una sezione in cui creiamo un’istanza e trasmettiamo un oggetto di impostazione. È personalizzabile, al momento del download compiliamo quella sezione con le impostazioni attuali del cliente.

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

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)


### Configurazione dell’SDK per web

La configurazione per l’SDK viene eseguita con la `configure` comando.

>[!IMPORTANT]
>
>`configure` è *sempre* il primo comando chiamato.

Esempio:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

È possibile impostare molte opzioni durante la configurazione. Di seguito sono riportate tutte le opzioni, raggruppate per categoria.

[Per saperne di più](../../fundamentals/configuring-the-sdk.md)


## Richiesta e rendering automatico delle offerte Target con caricamento pagina

### Utilizzo di at.js

Utilizzando at.js 2.x, se abiliti l’impostazione `pageLoadEnabled`, la libreria attiva una chiamata a Target Edge con `execute -> pageLoad`. Se tutte le impostazioni sono impostate sui valori predefiniti, non è necessaria alcuna codifica personalizzata. Una volta aggiunto at.js alla pagina e caricato dal browser, viene eseguita una chiamata Target Edge.

### Utilizzo dell’SDK per web

Contenuto creato in Adobe Target [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) può essere recuperato e riprodotto automaticamente dall&#39;SDK.

Per richiedere ed eseguire automaticamente il rendering delle offerte Target, utilizza la `sendEvent` e impostare `renderDecisions` opzione per `true`. In questo modo l’SDK renderà automaticamente qualsiasi contenuto personalizzato idoneo per il rendering automatico.

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

L&#39;SDK WEB di AEP invia automaticamente una notifica con le offerte eseguite dall&#39;SDK WEB. Questo è un esempio di come si presenta un payload della richiesta di notifica:

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

[Per saperne di più](../rendering-personalization-content.md)

## Come richiedere e NON eseguire il rendering automatico delle offerte Page Load Target

### Utilizzo di at.js

Sono disponibili due modi per attivare una chiamata a Target Edge per recuperare le offerte per il caricamento della pagina.

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

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)

### Utilizzo dell’SDK per web

Esegui un `sendEvent` comando con ambito speciale `decisionScopes`: `__view__`. Usiamo questo ambito come segnale per recuperare tutte le attività di caricamento pagina da Target e preacquisire tutte le visualizzazioni. L’SDK per web cercherà inoltre di valutare tutte le attività basate sulla visualizzazione del Compositore esperienza visivo. La disattivazione della preacquisizione della visualizzazione non è al momento supportata nell&#39;SDK per web.

Per accedere a qualsiasi contenuto di personalizzazione, puoi fornire una funzione di callback che verrà chiamata dopo che l’SDK ha ricevuto una risposta dal server riuscita. Al callback viene fornito un oggetto risultato, che può contenere la proprietà proposition contenente qualsiasi contenuto di personalizzazione restituito.

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

[Per saperne di più](../rendering-personalization-content.md#manually-rendering-content)


## Come richiedere mbox di Target basate su moduli specifiche


### Utilizzo di at.js

Puoi recuperare le attività del Compositore basato su moduli utilizzando `getOffer` funzione:

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

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html?lang=en)


### Utilizzo dell’SDK per web

Puoi recuperare le attività basate su Compositore basato su moduli utilizzando `sendEvent` e passando i nomi mbox sotto il `decisionScopes` opzione . La `sendEvent` restituisce una promessa risolta con un oggetto contenente le attività/proposizioni richieste: Questo è il modo in cui `propositions` l&#39;aspetto dell&#39;array è:

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

[Per saperne di più](../rendering-personalization-content.md#manually-rendering-content)

## Come applicare le attività di Target

### Utilizzo di at.js

Puoi applicare le attività Target utilizzando `applyOffers` funzione: `adobe.target.applyOffer(options)`

Esempio:

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html?lang=en)

### Utilizzo dell’SDK per web

Al momento questa funzione non è supportata nell’SDK per web.

## Come tenere traccia degli eventi

### Utilizzo di at.js

È possibile tenere traccia degli eventi utilizzando `trackEvent` o utilizzando `sendNotifications`.

Questa funzione genera una richiesta per segnalare le azioni dell&#39;utente, ad esempio clic e conversioni. Non fornisce attività nella risposta.


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

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=en)

### Utilizzo dell’SDK per web

Puoi tenere traccia di eventi e azioni utente chiamando il `sendEvent` comando, compilazione `_experience.decisioning.propositions` gruppo di campi XDM e impostazione `eventType` a uno dei 2 valori:

* `decisioning.propositionDisplay`: Segnala il rendering dell&#39;attività Target.
* `decisioning.propositionInteract`: Segnala un’interazione dell’utente con l’attività, ad esempio un clic del mouse.

La `_experience.decisioning.propositions` Il gruppo di campi XDM è una matrice di oggetti. Le proprietà di ciascun oggetto sono derivate dal `result.propositions` che viene restituito nel `sendEvent` comando: `{ id, scope, scopeDetails }`

**Esempio 1 - Tracciare una `decisioning.propositionDisplay` evento dopo il rendering di un&#39;attività**

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

**Esempio 2 - Tracciare una `decisioning.propositionInteract` evento dopo l’esecuzione di una metrica di clic**

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

[Per saperne di più](../rendering-personalization-content.md#manually-rendering-content)

## Come attivare una modifica di visualizzazione in un&#39;applicazione a pagina singola

### Utilizzo di at.js

Utilizza la `adobe.target.triggerView` funzione . È possibile chiamare questa funzione a ogni caricamento di una nuova pagina o quando si esegue di nuovo il rendering di un componente di una pagina. adobe.target.triggerView() deve essere implementato per le applicazioni a pagina singola (SPA) per utilizzare il Compositore esperienza visivo per creare test A/B e attività di targeting delle esperienze (XT). Se adobe.target.triggerView() non è implementato sul sito, non è possibile utilizzare il Compositore esperienza visivo per SPA.

**Esempio**

```javascript
adobe.target.triggerView("homeView")
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html?lang=en)


### Utilizzo dell’SDK per web

Per attivare o segnalare una modifica alla visualizzazione di un&#39;applicazione a pagina singola, imposta la `web.webPageDetails.viewName` sotto la `xdm` opzione `sendEvent` comando. L&#39;SDK WEB AEP controllerà la cache di visualizzazione, se sono presenti offerte per `viewName` specificato in `sendEvent` li eseguirà e invierà un evento di notifica della visualizzazione.

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

[Per saperne di più](./spa-implementation.md#implementing-xdm-views)

## Come sfruttare i token di risposta

Il contenuto di personalizzazione restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), che sono dettagli sull’attività, l’offerta, l’esperienza, il profilo utente, le informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

### Utilizzo di at.js

Utilizza gli eventi personalizzati at.js per ascoltare la risposta di Target e leggere i token di risposta.

**Esempio**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)


### Utilizzo dell’SDK per web

>[!IMPORTANT]
>
>Assicurati di utilizzare Platform Web SDK versione 2.6.0 o successiva.

I token di risposta vengono restituiti come parte del `propositions` che sono esposti nel risultato della `sendEvent` comando. Ogni proposta contiene un array di `items`e ogni elemento avrà un `meta` viene popolato con token di risposta se sono abilitati nell’interfaccia utente di amministrazione di Target. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)

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

[Per saperne di più](./accessing-response-tokens.md)

## Come gestire la visualizzazione momentanea di altri contenuti

### Utilizzo di at.js

Utilizzando at.js puoi gestire la visualizzazione momentanea di altri contenuti impostando `bodyHidingEnabled: true` in modo che at.js sia quello che si occuperebbe di nascondere anticipatamente i contenitori personalizzati prima che recuperi e applichi le modifiche DOM.
Le sezioni di pagina che contengono contenuto personalizzato possono essere nascoste ignorando at.js `bodyHiddenStyle`.
Per impostazione predefinita `bodyHiddenStyle` nasconde tutta la HTML `body`.
Entrambe le impostazioni possono essere ignorate utilizzando `window.targetGlobalSettings`. `window.targetGlobalSettings` deve essere posizionato prima di caricare at.js.

### Utilizzo dell’SDK per web

Con l’SDK per web, il cliente può impostare il proprio stile pre-hiding nel comando configura , come nell’esempio seguente:

```javascript
alloy("configure", {
  edgeConfigId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

Quando carichi l&#39;SDK web asincrono, consigliamo di inserire il seguente frammento nella pagina prima dell&#39;inserimento dell&#39;SDK web:

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

Esistono 2 tipi di log A4T supportati utilizzando at.js:

* Registrazione lato client di Analytics
* Registrazione lato server di Analytics

#### Registrazione lato client di Analytics

**Esempio 1: Utilizzo delle impostazioni globali di Target**

La registrazione lato client di Analytics può essere abilitata impostando `analyticsLogging: client_side` nelle impostazioni at.js o ignorando il `window.targetglobalSettings` oggetto.
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

Esempio 2: Configurazione in ogni `getOffers` funzione:

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

Il payload di risposta si presenta così:

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

La funzione di registrazione lato server di Analytics può essere abilitata impostando `analyticsLogging: server_side` nelle impostazioni at.js o ignorando il `window.targetglobalSettings` oggetto.
Quindi i dati scorrono come segue:

![](assets/a4t-server-side-atjs.png)

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=en)

### Utilizzo dell’SDK per web

L&#39;SDK per web supporta anche:

* Registrazione lato client di Analytics
* Registrazione lato server di Analytics

#### Registrazione lato client di Analytics

La registrazione lato client di Analytics è abilitata quando Adobe Analytics è disabilitato per quella configurazione DataStream.

![](assets/analytics-disabled-datastream-config.png)

Il cliente ha accesso al token Analytics (`tnta`) che deve essere condiviso con Analytics utilizzando [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)
in mediante concatenamento `sendEvent` e eseguire iterazioni attraverso la matrice delle proposizioni risultanti.

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

Ecco un diagramma che mostra il flusso di dati quando il lato client di Analytics è abilitato:

![](assets/analytics-client-side-logging.png)

#### Registrazione lato server di Analytics

La funzione di registrazione lato server di Analytics è abilitata quando Analytics è abilitato per la configurazione DataStream.

![](assets/analytics-enabled-datastream-config.png)

Quando la funzione di registrazione di analisi lato server è abilitata, il payload A4T che deve essere condiviso con Analytics in modo che il reporting di Analytics mostri le impression e le conversioni corrette venga condiviso a livello di Experience Edge, in modo che il cliente non debba eseguire ulteriori elaborazioni.

Ecco come i dati fluiscono nei nostri sistemi quando la funzione di registrazione di Analytics lato server è abilitata:

![](assets/analytics-server-side-logging.png)

## Come impostare le impostazioni globali di Target

### Utilizzo di at.js

Puoi sovrascrivere le impostazioni nella libreria at.js utilizzando`window.targetGlobalSettings`, anziché configurare le impostazioni nell’interfaccia utente di Target Standard/Premium o utilizzando le API REST.

La sostituzione deve essere definita prima che at.js sia caricato o in Amministrazione > Implementazione > Modifica impostazioni at.js > Impostazioni codice > Intestazione della libreria.

Esempio:

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en)

### Utilizzo dell’SDK per web

Questa funzione non è supportata nell’SDK per web.

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

### Utilizzo dell’SDK per web

Per aggiornare un profilo di Target, utilizza `sendEvent` e impostare `data.__adobe.target` proprietà, predefinizione dei nomi chiave utilizzando `profile`.

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
     "entity.productName": "T-shirt",
     "entity.productId": "1234"
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
            "entity.productName": "T-shirt",
            "entity.productId": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=en)


### Utilizzo dell’SDK per web

Per inviare i dati di Recommendations, utilizza la `sendEvent` e impostare `data.__adobe.target` proprietà, predefinizione dei nomi chiave utilizzando `entity`.

**Esempio**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.productName": "T-shirt",
        "entity.productId": "1234"
      }
    }
  }
});
```

## Come si utilizzano ID di terze parti

### Utilizzo di at.js

Utilizzando at.js sono disponibili diversi modi di invio `mbox3rdPartyId`, utilizzando `getOffer` o `getOffers`:

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

Oppure c&#39;è un modo per configurare il `mbox3rdPartyId` o `targetPageParams` o `targetPageParamsAll`.
Quando lo si imposta in `targetPageParams`, sarà inviato nelle richieste di `target-global-mbox` noto anche come `pag-lLoad`.
La raccomandazione deve essere impostata utilizzando `targetPageParamsAll` come verrà inviato in ogni richiesta target.
Il vantaggio di utilizzare `targetPageParamsAll` è possibile definire `mbox3rdPartyId` sulla pagina una volta e questo assicurerà che tutte le richieste target abbiano il diritto `mbox3rdPartyId`.

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

[Ulteriori informazioni](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=en)

### Utilizzo dell’SDK per web

L’SDK per web supporta l’ID di terze parti di Target. Tuttavia, richiede alcuni ulteriori passaggi. Prima di immergerci nella soluzione, dovremmo parlare un po&#39; di `identityMap`.
Identity Map consente ai clienti di inviare più identità. Tutte le identità sono a spazi dei nomi. Ogni namespace può avere una o più identità. Una particolare identità può essere contrassegnata come principale.
Tenendo presente queste informazioni, possiamo vedere quali sono i passaggi necessari per configurare l’sdk web per l’utilizzo dell’ID di terze parti di Target.

1. Imposta lo spazio dei nomi che conterrà l’ID di terze parti di Target nella vista Configurazione flusso di dati :

![](assets/mbox-3-party-id-setup.png)

1. Inviare lo spazio dei nomi di identità in ogni comando sendEvent in questo modo:

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

Utilizzando at.js sono disponibili 2 modi per configurare i token di proprietà, utilizzando `targetPageParams` o `targetPageParamsAll`. Utilizzo `targetPageParams` aggiunge il token di proprietà al `target-global-mbox` , ma utilizzando `targetPageParamsAll` aggiunge il token a tutte le chiamate di destinazione:

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

### Utilizzo dell’SDK per web

Utilizzando l’SDK per web, i clienti possono impostare la proprietà a un livello superiore, quando configuri la configurazione di Data Stream, nello spazio dei nomi Adobe Target:
![](assets/at-property-setup.png)
Questo significa che ogni chiamata di Target per la configurazione di Data Stream specifica conterrà quel token di proprietà.

## Come posso preacquisire le mbox

### Utilizzo di at.js

Questa funzionalità è disponibile solo in at.js 2.x. at.js 2.x ha una nuova funzione denominata `getOffers`. `getOffers` consentono ai clienti di preacquisire il contenuto per una o più mbox. Ecco un esempio:

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

NOTA: È vivamente consigliato garantire che ogni `mbox` in `mboxes` array ha un proprio indice. Di solito la prima mbox ha `index=0`, quello successivo `index=1`, ecc.

### Utilizzo dell’SDK per web

Questa funzionalità non è attualmente supportata nell&#39;SDK per web.

## Come eseguo il debug della mia implementazione di Target

### Utilizzo di at.js

At.js espone queste funzioni di debug:

* Disattivazione mbox: disattivare il recupero e il rendering di Target per verificare se la pagina è interrotta senza le interazioni di Target
* Debug mbox - at.js registra ogni azione
* Target Trace - con un token di traccia mbox generato in Bullseye è disponibile un oggetto trace con i dettagli che hanno partecipato al processo decisionale in `window.___target_trace` oggetto

Nota: Tutte queste funzioni di debug sono disponibili con funzionalità avanzate in [Debugger Adobe Experience Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

### Utilizzo dell’SDK per web

Quando utilizzi l’SDK per web, puoi utilizzare più funzionalità di debug:

* Utilizzo [Griffone](https://aep-sdks.gitbook.io/docs/beta/project-griffon)
* [Debug dell&#39;SDK per web abilitato](../../../edge/fundamentals/debugging.md)
* Utilizzo [Hook di monitoraggio SDK per web](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Utilizzo [Debugger Adobe Experience Platform](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=en)
* Traccia di destinazione
