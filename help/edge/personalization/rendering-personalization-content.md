---
title: Eseguire il rendering di contenuti personalizzati utilizzando l’SDK per web di Adobe Experience Platform
description: Scopri come eseguire il rendering di contenuti personalizzati con l’SDK per web di Adobe Experience Platform.
keywords: personalizzazione;renderdecisions;sendEvent;decisionScopes;proposizioni;
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 6ba563db7fd31084813426ffbb0c35be9d7fe4bb
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# Rendering di contenuti personalizzati

Adobe Experience Platform Web SDK supporta il recupero di contenuti personalizzati dalle soluzioni di personalizzazione Adobe, tra cui [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) e [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=it).

Inoltre, l’SDK per web abilita funzionalità di personalizzazione per pagina e pagina successiva tramite destinazioni di personalizzazione Adobe Experience Platform, ad esempio [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [connessione di personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md). Per scoprire come configurare un Experience Platform per la personalizzazione della stessa pagina e della pagina successiva, consulta la sezione [guida dedicata](../../destinations/ui/configure-personalization-destinations.md).

Contenuto creato in Adobe Target [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) può essere recuperato e riprodotto automaticamente dall&#39;SDK. Contenuto creato in Adobe Target [Compositore esperienza basato su moduli](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) L&#39;SDK non può eseguire il rendering automatico dell&#39;Offer decisioning o . Al contrario, devi richiedere questo contenuto utilizzando l’SDK e quindi eseguire manualmente il rendering del contenuto.

## Rendering automatico del contenuto

Quando invii eventi al server, puoi impostare la variabile `renderDecisions` opzione per `true`. In questo modo l’SDK renderà automaticamente qualsiasi contenuto personalizzato idoneo per il rendering automatico.

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

Il rendering di contenuti personalizzati è asincrono, pertanto non devi fare supposizioni su quando una particolare parte del contenuto avrà completato il rendering.

## Rendering manuale del contenuto

Per accedere a qualsiasi contenuto di personalizzazione, puoi fornire una funzione di callback che verrà chiamata dopo che l’SDK ha ricevuto una risposta dal server riuscita. Il callback viene fornito come `result` che può contenere un oggetto `propositions` contenente qualsiasi contenuto di personalizzazione restituito. Di seguito è riportato un esempio di come fornire una funzione di callback durante l&#39;invio di un evento.

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

In questo esempio, `result.propositions`, se esiste, è un array contenente proposizioni di personalizzazione relative all’evento. Per impostazione predefinita, include solo proposizioni idonee per il rendering automatico.

La `propositions` array può avere un aspetto simile a questo esempio:

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

Nell’esempio, la `renderDecisions` opzione non impostata su `true` quando `sendEvent` è stato eseguito, pertanto l&#39;SDK non ha tentato di eseguire automaticamente il rendering di alcun contenuto. Tuttavia, l’SDK ha ancora recuperato automaticamente il contenuto idoneo per il rendering automatico e, se lo desideri, ti ha fornito questo comando per il rendering manuale. Si noti che ogni oggetto proposizione ha la sua `renderAttempted` proprietà impostata su `false`.

In alternativa, imposta la variabile `renderDecisions` opzione per `true` quando invii l’evento, l’SDK avrebbe tentato di eseguire il rendering di tutte le proposte idonee per il rendering automatico (come descritto in precedenza). Di conseguenza, ogni oggetto della proposta ha il proprio `renderAttempted` proprietà impostata su `true`. In questo caso non sarebbe necessario eseguire manualmente il rendering di queste proposte.

Finora abbiamo discusso solo dei contenuti di personalizzazione idonei per il rendering automatico (ovvero di qualsiasi contenuto creato nel Compositore esperienza visivo di Adobe Target). Per recuperare qualsiasi contenuto di personalizzazione _not_ idoneo per il rendering automatico, è necessario richiedere il contenuto popolando il `decisionScopes` quando si invia l’evento. Un ambito è una stringa che identifica una particolare proposta che si desidera recuperare dal server.

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

In questo esempio, se le proposizioni si trovano sul server che corrispondono al `salutation` o `discount` sono restituiti e inclusi nell&#39;ambito `result.propositions` array. Tieni presente che le proposte idonee per il rendering automatico continueranno a essere incluse nella `propositions` array, indipendentemente da come si configura `renderDecisions` o `decisionScopes` opzioni. La `propositions` array, in questo caso, avrà un aspetto simile a questo esempio:

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

A questo punto, puoi eseguire il rendering del contenuto della proposta come ritieni opportuno. In questo esempio, la proposta corrispondente alla `discount` l&#39;ambito è una proposta di HTML creata utilizzando il Compositore esperienza basato su moduli di Adobe Target. Supponendo di avere un elemento nella pagina con l’ID di `daily-special` e desidera eseguire il rendering del contenuto dal `discount` proposta `daily-special` , procedi come segue:

1. Estrai le proposte dal `result` oggetto.
1. Sfogliare ogni proposta, cercando la proposta con un ambito di `discount`.
1. Se trovi una proposta, passa in rassegna ogni elemento della proposta, cercando l&#39;elemento che è contenuto di HTML. (È meglio controllare che assumere).
1. Se trovi un elemento contenente contenuto HTML, trova la `daily-special` nella pagina e sostituisci il relativo HTML con il contenuto personalizzato.
1. Dopo il rendering del contenuto, invia un `display` evento.

Il codice sarà il seguente:

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
>Se utilizzi Adobe Target, gli ambiti corrispondono alle mbox sul server, ma sono tutti richiesti contemporaneamente anziché singolarmente. La mbox globale viene sempre restituita.

### Gestione della visualizzazione momentanea di altri contenuti

L’SDK fornisce funzionalità per [gestisci visualizzazione momentanea](../personalization/manage-flicker.md) durante il processo di personalizzazione.
