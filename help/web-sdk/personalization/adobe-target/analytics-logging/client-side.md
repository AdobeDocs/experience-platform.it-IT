---
title: Registrazione lato client per i dati A4T in Platform Web SDK
description: Scopri come abilitare la registrazione lato client per Adobe Analytics for Target (A4T) utilizzando l’SDK web di Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;logging;web sdk;experience;platform;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Registrazione lato client per i dati A4T in Platform Web SDK

## Panoramica {#overview}

Adobe Experience Platform Web SDK consente di raccogliere i dati di [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) sul lato client dell&#39;applicazione Web.

La registrazione lato client indica che i dati [!DNL Target] rilevanti vengono restituiti sul lato client, consentendo di raccoglierli e condividerli con Analytics. Questa opzione deve essere abilitata se intendi inviare manualmente i dati ad Analytics utilizzando l&#39;[API di inserimento dati](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Un metodo per eseguire questa operazione utilizzando [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it) è attualmente in fase di sviluppo e sarà disponibile nel prossimo futuro.

Questo documento illustra i passaggi per impostare la registrazione A4T lato client per Web SDK e fornisce alcuni esempi di implementazione per i casi d’uso comuni.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che tu abbia familiarità con i concetti e i processi fondamentali relativi all’utilizzo dell’SDK web a scopo di personalizzazione. Per un&#39;introduzione, consulta la seguente documentazione:

* [Configurazione del Web SDK](/help/web-sdk/commands/configure/overview.md)
* [Invio di eventi](/help/web-sdk/commands/sendevent/overview.md)
* [Rendering del contenuto di personalizzazione](../../rendering-personalization-content.md)

## Configurare la registrazione lato client di Analytics {#set-up-client-side-logging}

Le seguenti sottosezioni descrivono come abilitare la registrazione lato client di Analytics per l’implementazione dell’SDK web.

### Abilita registrazione lato client di Analytics {#enable-analytics-client-side-logging}

Per considerare abilitata la registrazione lato client di Analytics per l&#39;implementazione, è necessario disabilitare la configurazione di Adobe Analytics nel [flusso di dati](../../../../datastreams/overview.md).

![Configurazione dello stream di dati di Analytics disabilitata](../assets/disable-analytics-datastream.png)

### Recupera i dati [!DNL A4T] dall&#39;SDK e inviali ad Analytics {#a4t-to-analytics}

Per il corretto funzionamento di questo metodo di reporting, è necessario inviare i dati correlati a [!DNL A4T] recuperati dal comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) nell&#39;hit di Analytics.

Quando Target Edge calcola una risposta di proposte, controlla se la registrazione lato client di Analytics è abilitata (ad esempio se Analytics è disabilitata nello stream di dati). Se la registrazione lato client è abilitata, il sistema aggiunge un token Analytics a ogni proposta nella risposta.

Il flusso è simile al seguente:

![Flusso di registrazione lato client](../assets/analytics-client-side-logging.png)

Di seguito è riportato un esempio di risposta `interact` quando la registrazione lato client di Analytics è abilitata. Se la proposta è per un&#39;attività che ha reporting di Analytics, avrà una proprietà `scopeDetails.characteristics.analyticsToken`.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Le proposte per le attività del Compositore esperienza basato su moduli possono contenere sia elementi di contenuto che elementi di metrica di clic sotto la stessa proposta. Pertanto, invece di avere un singolo token di analisi per la visualizzazione del contenuto nella proprietà `scopeDetails.characteristics.analyticsToken`, è possibile che nelle proprietà `scopeDetails.characteristics.analyticsDisplayToken` e `scopeDetails.characteristics.analyticsClickToken` siano specificati sia un token di analisi dei clic che un token di analisi dei clic.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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
            },
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
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Tutti i valori da `scopeDetails.characteristics.analyticsToken`, così come `scopeDetails.characteristics.analyticsDisplayToken` (per il contenuto visualizzato) e `scopeDetails.characteristics.analyticsClickToken` (per le metriche di clic) sono i payload A4T che devono essere raccolti e inclusi come tag `tnta` nella chiamata dell&#39;API di inserimento dati [5}.](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)

>[!IMPORTANT]
>
>Le proprietà `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` possono contenere più token, concatenati come una singola stringa delimitata da virgole.
>
>Negli esempi di implementazione forniti nella sezione successiva, più token di Analytics vengono raccolti iterativamente. Per concatenare un array di token di Analytics, utilizza una funzione simile alla seguente:
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Esempi di implementazione {#implementation-examples}

Le seguenti sottosezioni mostrano come implementare la registrazione lato client di Analytics per i casi d’uso comuni.

### Attività del Compositore esperienza basato su moduli {#form-based-composer}

È possibile utilizzare Web SDK per controllare l&#39;esecuzione delle proposte dalle attività [Compositore esperienza basato su Adobe Target Form](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

Quando richiedi proposte per un ambito decisionale specifico, la proposta restituita contiene il token Analytics appropriato. Si consiglia di concatenare il comando Platform Web SDK `sendEvent` e di eseguire iterazioni nelle proposte restituite per eseguirle durante la raccolta dei token di Analytics contemporaneamente.

È possibile attivare un comando `sendEvent` per un ambito di attività del Compositore esperienza basato su moduli come riportato di seguito:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Da qui, devi implementare il codice per eseguire le proposte e creare un payload che verrà infine inviato ad Analytics. Di seguito è riportato un esempio di ciò che `results.propositions` potrebbe contenere:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
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
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
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
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
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

Per estrarre il token Analytics da una proposta con elementi di contenuto, puoi implementare una funzione simile alla seguente:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Una proposta può avere diversi tipi di elementi, come indicato dalla proprietà `schema` dell&#39;elemento in questione. Per le attività del Compositore esperienza basato su moduli sono supportati quattro schemi di elementi delle proposte:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` e `JSON_SCHEMA` sono gli schemi che riflettono il tipo di offerta, mentre `MEASUREMENT_SCHEMA` riflette le metriche che devono essere collegate a un elemento DOM.

I payload di Analytics per le metriche di clic devono essere raccolti e inviati ad Analytics separatamente dagli elementi di contenuto, nel momento in cui il visitatore fa clic sul contenuto visualizzato in precedenza.

In questo caso, la seguente funzione di assistenza per ottenere i payload A4T della metrica di clic sarà utile:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Riepilogo dell’implementazione {#implementation-summary}

In sintesi, quando si applicano attività del Compositore esperienza basato su moduli con Platform Web SDK, è necessario eseguire i seguenti passaggi:

1. Invia un evento che recupera le offerte delle attività del Compositore esperienza basato su moduli;
1. Applica le modifiche al contenuto della pagina;
1. Invia l&#39;evento di notifica `decisioning.propositionDisplay`;
1. Raccogli i token di visualizzazione di Analytics dalla risposta SDK e crea un payload per l’hit di Analytics;
1. Invia il payload ad Analytics utilizzando l&#39;[API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Se nelle proposte distribuite sono presenti metriche di clic, i listener di clic devono essere configurati in modo che, quando viene eseguito un clic, invii l&#39;evento di notifica `decisioning.propositionInteract`. Il gestore `onBeforeEventSend` deve essere configurato in modo che quando si intercettano `decisioning.propositionInteract` eventi, si verifichino le seguenti azioni:
   1. Raccolta dei token di analisi dei clic da `xdm._experience.decisioning.propositions`
   1. Invio dell&#39;hit di analisi dei clic con il payload di Analytics raccolto tramite [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Attività del Compositore esperienza visivo {#visual-experience-composer-acitivties}

L&#39;SDK Web consente di gestire le offerte create con [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>I passaggi per l&#39;implementazione di questo caso d&#39;uso sono molto simili a quelli per [attività del Compositore esperienza basato su moduli](#form-based-composer). Per ulteriori informazioni, consulta la sezione precedente.

Quando è abilitato il rendering automatico, puoi raccogliere i token di Analytics dalle proposte che sono state eseguite sulla pagina. Si consiglia di concatenare il comando Platform Web SDK `sendEvent` e di eseguire l&#39;iterazione delle proposte restituite per filtrare quelle di cui l&#39;SDK Web ha tentato il rendering.

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
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Utilizzo di `onBeforeEventSend` per gestire le metriche della pagina {#using-onbeforeeventsend}

Utilizzando le attività di Adobe Target, puoi impostare metriche diverse sulla pagina, sia manualmente allegate al DOM che automaticamente associate al DOM (attività create dal Compositore esperienza visivo). Entrambi i tipi rappresentano un’interazione ritardata dell’utente finale sulla pagina web.

Per tenere conto di questo, la best practice prevede di raccogliere i payload di Analytics utilizzando l&#39;hook Web SDK di `onBeforeEventSend` Adobe Experience Platform. L&#39;hook `onBeforeEventSend` deve essere configurato utilizzando il comando `configure` e verrà riflesso in tutti gli eventi inviati tramite lo stream di dati.

Di seguito è riportato un esempio di come `onBeforeEventSent` può essere configurato per attivare gli hit di Analytics:

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Passaggi successivi {#next-steps}

Questa guida tratta la registrazione lato client per i dati A4T nell’SDK per web. Per ulteriori informazioni su come gestire i dati A4T nell&#39;Edge Network, consulta la guida alla [registrazione lato server](server-side.md).
