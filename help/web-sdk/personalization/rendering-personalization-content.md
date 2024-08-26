---
title: Eseguire il rendering di contenuti personalizzati utilizzando Adobe Experience Platform Web SDK
description: Scopri come eseguire il rendering di contenuti personalizzati con Adobe Experience Platform Web SDK.
keywords: personalizzazione;renderDecisions;sendEvent;decisionScopes;propositions;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# Rendering di contenuti personalizzati

Adobe Experience Platform Web SDK supporta il recupero di contenuti personalizzati dalle soluzioni di personalizzazione Adobe, tra cui [Adobe Target](https://business.adobe.com/it/products/target/adobe-target.html), [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it).

Inoltre, l&#39;SDK Web potenzia le funzionalità di personalizzazione della stessa pagina e della pagina successiva tramite destinazioni di personalizzazione Adobe Experience Platform, come [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e la [connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per informazioni su come configurare Experience Platform per la personalizzazione della stessa pagina e della pagina successiva, consulta la [guida dedicata](../../destinations/ui/activate-edge-personalization-destinations.md).

I contenuti creati nel [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) di Adobe Target e nell&#39;[interfaccia utente delle campagne web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) di Adobe Journey Optimizer possono essere recuperati e renderizzati automaticamente dall&#39;SDK. Il contenuto creato nel [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), nel [Canale esperienza basato su codice](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) o nell&#39;Offer decisioning di Adobe Target Adobe Journey Optimizer non può essere renderizzato automaticamente dall&#39;SDK. Devi invece richiedere questo contenuto utilizzando l’SDK e quindi eseguire manualmente il rendering del contenuto.

## Rendering automatico del contenuto {#automatic}

Quando si inviano eventi al server, è possibile impostare l&#39;opzione `renderDecisions` su `true`. In questo modo l’SDK deve eseguire automaticamente il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico.

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

## Rendering manuale del contenuto {#manual}

Per accedere a qualsiasi contenuto di personalizzazione, puoi fornire una funzione di callback che verrà chiamata dopo che l’SDK avrà ricevuto una risposta corretta dal server. Al callback viene fornito un oggetto `result`, che può contenere una proprietà `propositions` contenente qualsiasi contenuto di personalizzazione restituito. Di seguito è riportato un esempio di come fornire una funzione di callback durante l’invio di un evento.

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In questo esempio, `result.propositions`, se esiste, è un array contenente proposte di personalizzazione relative all&#39;evento. Per impostazione predefinita, include solo proposte idonee per il rendering automatico.

L&#39;array `propositions` potrebbe essere simile a questo esempio:

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

Nell&#39;esempio, l&#39;opzione `renderDecisions` non è stata impostata su `true` quando è stato eseguito il comando `sendEvent`, pertanto l&#39;SDK non ha tentato di eseguire automaticamente il rendering di alcun contenuto. L’SDK ha comunque recuperato automaticamente i contenuti idonei per il rendering automatico e ti ha fornito questo elemento per il rendering manuale, se lo desideri. Tieni presente che la proprietà `renderAttempted` di ogni oggetto della proposta è impostata su `false`.

Se invece avresti impostato l&#39;opzione `renderDecisions` su `true` durante l&#39;invio dell&#39;evento, l&#39;SDK avrebbe tentato di eseguire il rendering di tutte le proposte idonee per il rendering automatico (come descritto in precedenza). Di conseguenza, la proprietà `renderAttempted` di ciascuno degli oggetti della proposta sarà impostata su `true`. In questo caso, non sarebbe necessario eseguire manualmente il rendering di queste proposte.

Finora abbiamo discusso solo dei contenuti di personalizzazione idonei al rendering automatico (ovvero qualsiasi contenuto creato nel Compositore esperienza visivo di Adobe Target o nell’interfaccia utente delle campagne web di Adobe Journey Optimizer). Per recuperare qualsiasi contenuto di personalizzazione _non_ idoneo per il rendering automatico, è necessario richiedere il contenuto compilando l&#39;opzione `decisionScopes` durante l&#39;invio dell&#39;evento. Un ambito è una stringa che identifica una particolare proposta che desideri recuperare dal server.

Ecco un esempio:

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In questo esempio, se le proposte vengono trovate nel server corrispondente all&#39;ambito `salutation` o `discount`, vengono restituite e incluse nell&#39;array `result.propositions`. Tieni presente che le proposte idonee per il rendering automatico continueranno a essere incluse nell&#39;array `propositions`, indipendentemente da come configuri le opzioni `renderDecisions` o `decisionScopes`. L&#39;array `propositions`, in questo caso, sarà simile all&#39;esempio seguente:

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

A questo punto, puoi eseguire il rendering del contenuto delle proposte come lo ritieni opportuno. In questo esempio, la proposta corrispondente all&#39;ambito `discount` è una proposta HTML creata utilizzando il Compositore esperienza basato su moduli di Adobe Target. Se nella pagina è presente un elemento con ID `daily-special` e si desidera eseguire il rendering del contenuto della proposta `discount` nell&#39;elemento `daily-special`, eseguire le operazioni seguenti:

1. Estrarre le proposte dall&#39;oggetto `result`.
1. Eseguire un ciclo in ogni proposta, cercando la proposta con un ambito di `discount`.
1. Se trovi una proposta, scorri ciclicamente ogni elemento della proposta, cercando l’elemento che è il contenuto HTML. (È meglio controllare che presumere.)
1. Se trovi un elemento contenente contenuti HTML, individua l&#39;elemento `daily-special` nella pagina e sostituisci il relativo HTML con il contenuto personalizzato.
1. Dopo il rendering del contenuto, invia un evento `display`.

Il codice si presenterà come segue:

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
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

L&#39;SDK fornisce funzionalità per [gestire la visualizzazione momentanea di altri contenuti](../personalization/manage-flicker.md) durante il processo di personalizzazione.

## Rendering delle proposte in applicazioni a pagina singola senza incrementare le metriche {#applypropositions}

Il comando `applyPropositions` consente di eseguire il rendering o l&#39;esecuzione di un array di proposte da [!DNL Target] o Adobe Journey Optimizer in applicazioni a pagina singola, senza incrementare le metriche [!DNL Analytics] e [!DNL Target]. Questo aumenta l’accuratezza della generazione di rapporti.

>[!IMPORTANT]
>
>Se le proposte per l&#39;ambito `__view__` (o una superficie Web) sono state sottoposte a rendering al caricamento della pagina, il relativo flag `renderAttempted` verrà impostato su `true`. Il comando `applyPropositions` non eseguirà nuovamente il rendering delle proposte di ambito `__view__` (o superficie Web) che presentano il flag `renderAttempted: true`.

### Caso d’uso 1: rieseguire il rendering delle proposte di visualizzazione di un’applicazione a pagina singola

Il caso d’uso descritto nell’esempio seguente riproduce le proposte di visualizzazione del carrello recuperate e sottoposte a rendering in precedenza senza inviare notifiche di visualizzazione.

Nell&#39;esempio seguente, il comando `sendEvent` viene attivato in seguito a una modifica della visualizzazione e salva l&#39;oggetto risultante in una costante.

Successivamente, quando la visualizzazione o un componente viene aggiornato, viene chiamato il comando `applyPropositions`, con le proposte del precedente comando `sendEvent`, per eseguire nuovamente il rendering delle proposte di visualizzazione.

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
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
    "propositions": cartPropositions
});
```

### Caso d’uso 2: proposte di rendering prive di selettore

Questo caso d&#39;uso si applica alle esperienze create utilizzando [!DNL Target Form-based Experience Composer] o il [canale di esperienza basato su codice](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) di Adobe Journey Optimizer.

È necessario fornire il selettore, l&#39;azione e l&#39;ambito nella chiamata `applyPropositions`.

`actionTypes` supportati sono:

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

            alloy("sendEvent", {
                "xdm": {
                    "eventType": "decisioning.propositionDisplay",
                    "_experience": {
                        "decisioning": {
                            "propositions": [{
                              	"id": id,
                                "scope": scope,
                              	"scopeDetails": scopeDetails
                            }],
                            "propositionEventType": {
                                "display": 1
                            }
                        }
                    }
                }
            });
        }
    });
});
```

Se non fornisci metadati per un ambito decisionale, le proposte associate non verranno sottoposte a rendering.
