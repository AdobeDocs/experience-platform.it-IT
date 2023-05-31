---
title: Eseguire il rendering di contenuti personalizzati utilizzando Adobe Experience Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Adobe Experience Platform Web SDK.
keywords: personalizzazione;renderDecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# Rendering di contenuti personalizzati

Adobe Experience Platform Web SDK supporta il recupero di contenuti personalizzati dalle soluzioni di personalizzazione Adobe, tra cui [Adobe Target](https://business.adobe.com/it/products/target/adobe-target.html), [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it).

Inoltre, l’SDK per web fornisce funzionalità di personalizzazione per la stessa pagina e per la pagina successiva tramite destinazioni di personalizzazione Adobe Experience Platform, come [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per informazioni su come configurare l’Experience Platform per la personalizzazione della stessa pagina e della pagina successiva, consulta [guida dedicata](../../destinations/ui/activate-edge-personalization-destinations.md).

Contenuto creato in Adobe Target [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) e ADOBE JOURNEY OPTIMIZER [Interfaccia utente di Web Campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) può essere recuperato e renderizzato automaticamente dall’SDK. Contenuto creato in Adobe Target [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) o Offer decisioning non può essere renderizzato automaticamente dall’SDK. Devi invece richiedere questo contenuto utilizzando l’SDK e quindi eseguire manualmente il rendering del contenuto.

## Rendering automatico del contenuto

Quando invii eventi al server, puoi impostare `renderDecisions` opzione per `true`. In questo modo l’SDK deve eseguire automaticamente il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico.

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

Il rendering di contenuti personalizzati è asincrono, pertanto non devi fare supposizioni su quando un particolare contenuto avrà completato il rendering.

## Rendering manuale del contenuto

Per accedere a qualsiasi contenuto di personalizzazione, puoi fornire una funzione di callback che verrà chiamata dopo che l’SDK avrà ricevuto una risposta corretta dal server. Il callback viene fornito come `result` oggetto, che può contenere `propositions` contenente eventuali contenuti di personalizzazione restituiti. Di seguito è riportato un esempio di come fornire una funzione di callback durante l’invio di un evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In questo esempio, `result.propositions`, se esiste, è un array contenente proposte di personalizzazione relative all’evento. Per impostazione predefinita, include solo proposte idonee per il rendering automatico.

Il `propositions` l’array potrebbe essere simile a questo esempio:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

Nell’esempio, il `renderDecisions` opzione non impostata su `true` quando `sendEvent` L&#39;SDK non ha tentato di eseguire automaticamente il rendering di alcun contenuto. L’SDK ha comunque recuperato automaticamente i contenuti idonei per il rendering automatico e ti ha fornito questo elemento per il rendering manuale, se lo desideri. Tieni presente che ogni oggetto della proposta ha il proprio `renderAttempted` proprietà impostata su `false`.

Se invece avresti impostato `renderDecisions` opzione per `true` durante l’invio dell’evento, l’SDK avrebbe tentato di eseguire il rendering di qualsiasi proposta idonea per il rendering automatico (come descritto in precedenza). Di conseguenza, ogni oggetto della proposta avrebbe il suo `renderAttempted` proprietà impostata su `true`. In questo caso, non sarebbe necessario eseguire manualmente il rendering di queste proposte.

Finora abbiamo discusso solo dei contenuti di personalizzazione idonei al rendering automatico (ovvero qualsiasi contenuto creato nel Compositore esperienza visivo di Adobe Target o nell’interfaccia utente delle campagne web di Adobe Journey Optimizer). Per recuperare eventuali contenuti di personalizzazione _non_ idonei per il rendering automatico, è necessario richiedere il contenuto compilando il `decisionScopes` durante l’invio dell’evento. Un ambito è una stringa che identifica una particolare proposta che desideri recuperare dal server.

Ecco un esempio:

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In questo esempio, se le proposte si trovano sul server che corrisponde a `salutation` o `discount` , vengono restituiti e inclusi nel `result.propositions` array. Tieni presente che le proposte idonee per il rendering automatico continueranno a essere incluse nel `propositions` , indipendentemente dalla modalità di configurazione `renderDecisions` o `decisionScopes` opzioni. Il `propositions` L’array, in questo caso, sarà simile a questo esempio:

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

A questo punto, puoi eseguire il rendering del contenuto delle proposte come lo ritieni opportuno. In questo esempio, la proposta corrisponde alla `discount` scope è una proposta HTML creata utilizzando il Compositore esperienza basato su moduli di Adobe Target. Supponendo di avere un elemento nella pagina con l&#39;ID di `daily-special` e desiderano eseguire il rendering del contenuto da `discount` proposizione nel `daily-special` eseguire le operazioni seguenti:

1. Estrarre proposte dalla `result` oggetto.
1. Eseguire un ciclo tra le proposte, cercando la proposta con un ambito di `discount`.
1. Se trovi una proposta, scorri ciclicamente ogni elemento della proposta, cercando l’elemento che è il contenuto HTML. (È meglio controllare che presumere.)
1. Se trovi un elemento contenente contenuti HTML, individua `daily-special` nella pagina e sostituirne il HTML con il contenuto personalizzato.
1. Dopo il rendering del contenuto, invia un `display` evento.

Il codice si presenterà come segue:

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
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

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
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


>[!TIP]
>
>Se utilizzi Adobe Target, gli ambiti corrispondono agli elementi mbox sul server, tranne per il fatto che sono tutti richiesti contemporaneamente anziché singolarmente. La mbox globale viene sempre restituita.

### Gestisci visualizzazione momentanea di altri contenuti

L’SDK fornisce servizi per: [gestisci visualizzazione momentanea di altri contenuti](../personalization/manage-flicker.md) durante il processo di personalizzazione.

## Rendering delle proposte in applicazioni a pagina singola senza incrementare le metriche {#applypropositions}

Il `applyPropositions` consente di eseguire il rendering o l’esecuzione di un array di proposte da [!DNL Target] nelle applicazioni a pagina singola, senza incrementare [!DNL Analytics] e [!DNL Target] metriche. Questo aumenta l’accuratezza della generazione di rapporti.

>[!IMPORTANT]
>
>Se le proposte per `__view__` l&#39;ambito (o una superficie web) è stato sottoposto a rendering al caricamento della pagina, il `renderAttempted` il flag verrà impostato su `true`. Il `applyPropositions` il comando non rieseguirà il rendering del `__view__` le proposte di ambito (o superficie web) che presentano `renderAttempted: true` flag.

### Caso d’uso 1: rieseguire il rendering delle proposte di visualizzazione di un’applicazione a pagina singola

Il caso d’uso descritto nell’esempio seguente riproduce le proposte di visualizzazione del carrello recuperate e sottoposte a rendering in precedenza senza inviare notifiche di visualizzazione.

Nell’esempio seguente, il `sendEvent` viene attivato in seguito a una modifica della vista e salva l&#39;oggetto risultante in una costante.

Successivamente, quando la vista o un componente viene aggiornato, il `applyPropositions` viene chiamato, con le proposte del precedente `sendEvent` per eseguire nuovamente il rendering delle proposte di visualizzazione.

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### Caso d’uso 2: proposte di rendering prive di selettore

Questo caso d’uso si applica alle offerte di attività create utilizzando [!DNL Target Form-based Experience Composer].

Devi fornire il selettore, l&#39;azione e l&#39;ambito nella `applyPropositions` chiamare.

Supportato `actionTypes` sono:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

Se non fornisci metadati per un ambito decisionale, le proposte associate non verranno sottoposte a rendering.
