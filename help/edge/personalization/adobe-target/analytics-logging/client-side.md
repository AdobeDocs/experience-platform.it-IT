---
title: Registrazione lato client per i dati A4T nell’SDK per web di Platform
description: Scopri come abilitare la registrazione lato client per Adobe Analytics for Target (A4T) utilizzando l’SDK per web di Experience Platform.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;registrazione;sdk web;esperienza;piattaforma;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: de420d3bbf35968fdff59b403a0f2b18110f3c17
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 3%

---

# Registrazione lato client per i dati A4T nell’SDK per web di Platform

## Panoramica {#overview}

L’SDK web Adobe Experience Platform ti consente di raccogliere [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) sul lato client dell&#39;applicazione web.

Registrazione sul lato client: [!DNL Target] i dati vengono restituiti sul lato client, consentendoti di raccoglierli e condividerli con Analytics. Questa opzione deve essere attivata se intendi inviare manualmente i dati ad Analytics utilizzando [API di inserimento dati](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Un metodo per eseguire questa operazione utilizzando [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it) è attualmente in fase di sviluppo e sarà disponibile a breve.

Questo documento descrive i passaggi per la configurazione della registrazione A4T lato client per l’SDK per web e fornisce alcuni esempi di implementazione per i casi d’uso comuni.

## Prerequisiti {#prerequisites}

Questa esercitazione presuppone che tu abbia familiarità con i concetti e i processi fondamentali relativi all’utilizzo dell’SDK per web a scopo di personalizzazione. Per un’introduzione, consulta la seguente documentazione:

* [Configurazione dell’SDK per web](../../../fundamentals/configuring-the-sdk.md)
* [Invio di eventi](../../../fundamentals/tracking-events.md)
* [Rendering del contenuto di personalizzazione](../../rendering-personalization-content.md)

## Configurare la registrazione lato client di Analytics {#set-up-client-side-logging}

Le sottosezioni seguenti descrivono come abilitare la registrazione lato client di Analytics per l’implementazione dell’SDK per web.

### Abilitare la registrazione lato client di Analytics {#enable-analytics-client-side-logging}

Per considerare la registrazione lato client di Analytics abilitata per la tua implementazione, devi disabilitare la configurazione Adobe Analytics nella tua [datastream](../../../datastreams/overview.md).

![Configurazione del datastream di Analytics disabilitata](../assets/disable-analytics-datastream.png)

### Recupera [!DNL A4T] dati dall’SDK e inviarli ad Analytics {#a4t-to-analytics}

Affinché questo metodo di reporting funzioni correttamente, devi inviare il [!DNL A4T] dati correlati recuperati da [`sendEvent`](../../../fundamentals/tracking-events.md) nell’hit di Analytics.

Quando Target Edge calcola una risposta a proposte, controlla se la registrazione lato client di Analytics è abilitata (ovvero se Analytics è disabilitato nel datastream). Se la registrazione lato client è abilitata, il sistema aggiunge un token Analytics a ogni proposta nella risposta.

Il flusso è simile al seguente:

![Flusso di registrazione lato client](../assets/analytics-client-side-logging.png)

Di seguito è riportato un esempio di `interact` quando la registrazione lato client di Analytics è abilitata. Se la proposta è per un’attività con reporting di Analytics, avrà una `scopeDetails.characteristics.analyticsToken` proprietà.

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

Le proposte per le attività del Compositore esperienza basato su moduli possono contenere sia contenuto che elementi di metrica clic sotto la stessa proposta. Pertanto, invece di avere un singolo token di analisi per la visualizzazione del contenuto in `scopeDetails.characteristics.analyticsToken` possono avere sia un token di analisi di visualizzazione che un token di analisi di clic specificato in `scopeDetails.characteristics.analyticsDisplayToken` e `scopeDetails.characteristics.analyticsClickToken` proprietà, di conseguenza.

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

Tutti i valori da `scopeDetails.characteristics.analyticsToken`, nonché `scopeDetails.characteristics.analyticsDisplayToken` (per il contenuto visualizzato) e `scopeDetails.characteristics.analyticsClickToken` (per le metriche di clic) sono i payload A4T che devono essere raccolti e inclusi come `tnta` in [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) chiama.

>[!IMPORTANT]
>
>La `analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` Le proprietà possono contenere più token, concatenati come una singola stringa delimitata da virgole.
>
>Negli esempi di implementazione forniti nella sezione successiva, più token Analytics vengono raccolti in modo iterativo. Per concatenare un array di token di Analytics, utilizza una funzione simile alla seguente:
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Esempi di implementazione {#implementation-examples}

Le sottosezioni seguenti mostrano come implementare la registrazione lato client di Analytics per i casi d’uso comuni.

### Attività del Compositore esperienza basato su moduli {#form-based-composer}

Puoi usare l’SDK per web per controllare l’esecuzione di proposizioni da [Compositore esperienza basato su moduli di Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) attività.

Quando richiedi le proposte per un ambito decisionale specifico, la proposta restituita contiene il token Analytics appropriato. La best practice prevede la catena dell’SDK per web di Platform `sendEvent` esegui il comando e ripeti le proposizioni restituite per eseguirle durante la raccolta dei token di Analytics allo stesso tempo.

Puoi attivare un `sendEvent` comando per un ambito di attività del Compositore esperienza basato su moduli come questo:

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

Da qui, devi implementare il codice per eseguire le proposizioni e creare un payload che verrà infine inviato ad Analytics. Questo è un esempio di cosa `results.propositions` potrebbero contenere:

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

Per estrarre il token di Analytics da una proposta con elementi di contenuto, puoi implementare una funzione simile alla seguente:

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

Una proposta può avere diversi tipi di elementi, come indicato dalla `schema` proprietà dell&#39;elemento in questione. Sono disponibili quattro schemi di elementi di proposta supportati per le attività del Compositore esperienza basato su moduli:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` e `JSON_SCHEMA` sono gli schemi che riflettono il tipo di offerta, mentre `MEASUREMENT_SCHEMA` riflette le metriche che devono essere collegate a un elemento DOM.

I payload di Analytics per le metriche di clic devono essere raccolti e inviati ad Analytics separatamente dagli elementi di contenuto, nel momento in cui il visitatore fa clic sul contenuto visualizzato in precedenza.

In questo caso, la seguente funzione helper per per ottenere i payload A4T della metrica di clic sarà utile:

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

#### Riepilogo dell&#39;implementazione {#implementation-summary}

In sintesi, è necessario eseguire i seguenti passaggi durante l’applicazione delle attività del Compositore esperienza basato su moduli con l’SDK per web di Platform:

1. Inviare un evento che recupera le offerte di attività del Compositore esperienza basato su moduli;
1. Applicare le modifiche al contenuto della pagina;
1. Invia `decisioning.propositionDisplay` evento di notifica;
1. raccogliere i token di visualizzazione di Analytics dalla risposta SDK e creare un payload per l’hit di Analytics;
1. Invia il payload ad Analytics utilizzando [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Se nelle proposte consegnate sono presenti metriche di clic, è necessario impostare gli ascoltatori di clic in modo che, quando si esegue un clic, invii il `decisioning.propositionInteract` evento di notifica. La `onBeforeEventSend` deve essere configurato in modo che durante l&#39;intercettazione `decisioning.propositionInteract` , si verificano le seguenti azioni:
   1. Raccolta dei token di clic su Analytics da `xdm._experience.decisioning.propositions`
   1. Invio dell’hit di clic su Analytics con il payload di Analytics raccolto tramite [API di inserimento dati](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

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

L’SDK per web ti consente di gestire le offerte create utilizzando [Compositore esperienza visivo](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>I passaggi per l’implementazione di questo caso d’uso sono molto simili ai passaggi per [Attività del Compositore esperienza basato su moduli](#form-based-composer). Per ulteriori informazioni, consulta la sezione precedente.

Quando il rendering automatico è abilitato, puoi raccogliere i token Analytics dalle proposizioni eseguite sulla pagina. La best practice prevede la catena dell’SDK per web di Platform `sendEvent` esegui il comando e ripeti le proposizioni restituite per filtrare quelle che l&#39;SDK per web ha tentato di eseguire il rendering.

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

### Utilizzo `onBeforeEventSend` per gestire le metriche di pagina {#using-onbeforeeventsend}

Utilizzando le attività di Adobe Target, puoi impostare diverse metriche sulla pagina, manualmente allegate al DOM o automaticamente allegate al DOM (VEC Authored Activities). Entrambi i tipi sono un’interazione ritardata dell’utente finale sulla pagina web.

Per tenere conto di ciò, la best practice consiste nel raccogliere i payload di Analytics utilizzando `onBeforeEventSend` Gancio Adobe Experience Platform Web SDK. La `onBeforeEventSend` il gancio deve essere configurato utilizzando `configure` e verranno riflessi in tutti gli eventi inviati attraverso il datastream.

Di seguito è riportato un esempio di come `onBeforeEventSent` può essere configurato per attivare gli hit di Analytics:

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
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

Questa guida ha trattato la registrazione lato client per i dati A4T nell’SDK per web. Consulta la guida su [registrazione lato server](server-side.md) per ulteriori informazioni su come gestire i dati A4T su Edge Network.
