---
title: Tipi di eventi nell’estensione Adobe Experience Platform Web SDK
description: Scopri come utilizzare i tipi di evento forniti dall’estensione Adobe Experience Platform Web SDK in Adobe Experience Platform Launch.
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# Tipi di evento

Questa pagina descrive i tipi di evento Adobe Experience Platform forniti dall’estensione tag Adobe Experience Platform Web SDK. Questi sono utilizzati per [regole di compilazione](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) e non devono essere confusi con `eventType` campo in [`xdm` oggetto](/help/web-sdk/commands/sendevent/xdm.md).

## [!UICONTROL Invio evento completato]

In genere, la proprietà ha una o più regole che utilizzano [[!UICONTROL Invia evento] azione](action-types.md#send-event) per inviare eventi a Adobe Experience Platform Edge Network. Ogni volta che un evento viene inviato a Edge Network, viene restituita una risposta al browser con dati utili. Senza [!UICONTROL Invio evento completato] tipo di evento, non avresti accesso ai dati restituiti.

Per accedere ai dati restituiti, crea una regola separata, quindi aggiungi un [!UICONTROL Invio evento completato] alla regola. Questa regola viene attivata ogni volta che viene ricevuta una risposta corretta dal server a seguito di una [!UICONTROL Invia evento] azione.

Quando un [!UICONTROL Invio evento completato] evento attiva una regola, fornisce i dati restituiti dal server che possono essere utili per eseguire determinate attività. In genere, si aggiunge un [!UICONTROL Codice personalizzato] azione (da [!UICONTROL Core] ) alla stessa regola che contiene il [!UICONTROL Invio evento completato] evento. In [!UICONTROL Codice personalizzato] , il codice personalizzato avrà accesso a una variabile denominata `event`. Questo `event` conterrà i dati restituiti dal server.

La regola per la gestione dei dati restituiti da Edge Network potrebbe essere simile alla seguente:

![](assets/send-event-complete.png)

Di seguito sono riportati alcuni esempi di come eseguire determinate attività utilizzando [!UICONTROL Codice personalizzato] in questa regola.

### Rendering manuale di contenuti personalizzati

Nell’azione Codice personalizzato, inclusa nella regola per la gestione dei dati di risposta, puoi accedere alle proposte di personalizzazione restituite dal server. A questo scopo, digita il seguente codice personalizzato:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` esiste, è un array contenente oggetti della proposta di personalizzazione. Le proposte incluse nell’array sono determinate, in gran parte, dal modo in cui l’evento è stato inviato al server.

Per questo primo scenario, supponiamo che tu non abbia selezionato [!UICONTROL Decisioni di rendering] e non hanno fornito alcun [!UICONTROL ambiti decisionali] all&#39;interno del [!UICONTROL Invia evento] azione responsabile dell’invio dell’evento.

![img.png](assets/send-event-render-unchecked-without-scopes.png)

In questo esempio, la proprietà `propositions` l’array contiene solo proposte relative all’evento idonee per il rendering automatico.

Il `propositions` l’array potrebbe assomigliare a questo esempio:

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
    "renderAttempted": false
  }
]
```

Durante l’invio dell’evento, il [!UICONTROL Decisioni di rendering] La casella di controllo non è stata selezionata, pertanto l’SDK non ha tentato di eseguire automaticamente il rendering di alcun contenuto. L’SDK ha comunque recuperato automaticamente i contenuti idonei per il rendering automatico e ti ha fornito come eseguire il rendering manualmente, se lo desideri. Tieni presente che ogni oggetto della proposta ha il proprio `renderAttempted` proprietà impostata su `false`.

Se invece avresti selezionato [!UICONTROL Decisioni di rendering] Quando inviava l’evento, l’SDK tentava di eseguire il rendering di tutte le proposte idonee per il rendering automatico. Di conseguenza, ogni oggetto della proposta avrebbe il suo `renderAttempted` proprietà impostata su `true`. In questo caso, non sarebbe necessario eseguire manualmente il rendering di queste proposte.

Finora hai esaminato solo i contenuti di personalizzazione idonei per il rendering automatico (ad esempio, qualsiasi contenuto creato nel Compositore esperienza visivo di Adobe Target). Per recuperare eventuali contenuti di personalizzazione _non_ idonei per il rendering automatico, richiedi il contenuto fornendo ambiti decisionali utilizzando [!UICONTROL Ambiti decisionali] campo in [!UICONTROL Invia evento] azione. Un ambito è una stringa che identifica una particolare proposta che desideri recuperare dal server.

Il [!UICONTROL Invia evento] L&#39;azione sarà simile alla seguente:

![img.png](assets/send-event-render-unchecked-with-scopes.png)

In questo esempio, se le proposte si trovano sul server che corrisponde a `salutation` o `discount` , vengono restituiti e inclusi nel `propositions` array. Tieni presente che le proposte idonee per il rendering automatico continueranno a essere incluse nel `propositions` , indipendentemente dalla modalità di configurazione [!UICONTROL Decisioni di rendering] o [!UICONTROL Ambiti decisionali] campi in [!UICONTROL Invia evento] azione. Il `propositions` L’array, in questo caso, sarà simile a questo esempio:

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
    "renderAttempted": false
  }
]
```

A questo punto, puoi eseguire il rendering del contenuto delle proposte come lo ritieni opportuno. In questo esempio, la proposta corrisponde alla `discount` scope è una proposta HTML creata utilizzando il Compositore esperienza basato su moduli di Adobe Target. Supponiamo di avere un elemento sulla pagina con l&#39;ID di `daily-special` e desiderano eseguire il rendering del contenuto da `discount` proposizione nel `daily-special` elemento. Effettua le seguenti operazioni:

1. Estrarre proposte dalla `event` oggetto.
1. Eseguire un ciclo tra le proposte, cercando la proposta con un ambito di `discount`.
1. Se trovi una proposta, scorri ciclicamente ogni elemento della proposta, cercando l’elemento che è il contenuto HTML. (È meglio controllare che presumere.)
1. Se trovi un elemento contenente contenuti HTML, individua `daily-special` nella pagina e sostituirne il HTML con il contenuto personalizzato.

Il codice personalizzato all&#39;interno del [!UICONTROL Codice personalizzato] L&#39;azione potrebbe essere visualizzata come segue:

```javascript
var propositions = event.propositions;

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
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### Accesso ai token di risposta di Adobe Target

Il contenuto di personalizzazione restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), ovvero dettagli sull’attività, l’offerta, l’esperienza, il profilo utente, le informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

Nell’azione Codice personalizzato, inclusa nella regola per la gestione dei dati di risposta, puoi accedere alle proposte di personalizzazione restituite dal server. A tale scopo, digita il seguente codice personalizzato:

```javascript
var propositions = event.propositions;
```

Se `event.propositions` esiste, è un array contenente oggetti della proposta di personalizzazione. Consulta [Rendering manuale di contenuti personalizzati](#manually-render-personalized-content) per ulteriori informazioni sul contenuto di `result.propositions`.

Supponiamo di voler raccogliere tutti i nomi delle attività da tutte le proposte di cui è stato eseguito il rendering automatico dall’SDK web e inviarli in un singolo array. È quindi possibile inviare il singolo array a una terza parte. In questo caso, scrivi il codice personalizzato all’interno del [!UICONTROL Codice personalizzato] azione per:

1. Estrarre proposte dalla `event` oggetto.
1. Eseguire un ciclo tra le proposte.
1. Determina se l’SDK ha eseguito il rendering della proposta.
1. In tal caso, scorri ciclicamente ogni elemento della proposta.
1. Recupera il nome dell’attività da `meta` , che è un oggetto contenente token di risposta.
1. Invia il nome dell’attività a un array.
1. Invia i nomi delle attività a una terza parte.

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```
