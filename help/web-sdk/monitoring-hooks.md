---
title: Hook di monitoraggio per Adobe Experience Platform Web SDK
description: Scopri come utilizzare gli hook di monitoraggio forniti da Adobe Experience Platform Web SDK per eseguire il debug dell’implementazione e acquisire i registri Web SDK.
source-git-commit: 3dacc991fd7760c1c358bec07aca83ffeb4f4f4d
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---


# Monitoraggio degli hook per Web SDK

Adobe Experience Platform Web SDK include hook di monitoraggio utilizzabili per monitorare vari eventi di sistema. Questi strumenti sono utili per sviluppare strumenti di debug personalizzati e per acquisire i registri dell’SDK web.

Web SDK attiva le funzioni di monitoraggio indipendentemente dal fatto che sia stato abilitato il [debug](commands/configure/debugenabled.md).

## `onInstanceCreated` {#onInstanceCreated}

Questa funzione di callback viene attivata quando è stata creata correttamente una nuova istanza di Web SDK. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.instance` | Funzione | Funzione di istanza utilizzata per chiamare i comandi Web SDK. |

## `onInstanceConfigured` {#onInstanceConfigured}

Questa funzione di callback viene attivata dall&#39;SDK Web quando il comando [`configure`](commands/configure/overview.md) è stato risolto. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.config` | Oggetto | Oggetto contenente la configurazione utilizzata per l’istanza Web SDK. Queste sono le opzioni passate al comando [`configure`](commands/configure/overview.md) con tutti i valori predefiniti aggiunti. |

## `onBeforeCommand` {#onBeforeCommand}

Questa funzione di callback viene attivata da Web SDK prima dell&#39;esecuzione di qualsiasi altro comando. È possibile utilizzare questa funzione per recuperare le opzioni di configurazione di un comando specifico. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.commandName` | Stringa | Nome del comando Web SDK prima del quale viene eseguita questa funzione. |
| `data.options` | Oggetto | Oggetto contenente le opzioni passate al comando Web SDK. |

## `onCommandResolved` {#onCommandResolved}

Questa funzione di callback viene attivata quando si risolvono le promesse di comando. È possibile utilizzare questa funzione per visualizzare le opzioni e i risultati del comando. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.commandName` | Stringa | Nome del comando Web SDK eseguito. |
| `data.options` | Oggetto | Oggetto contenente le opzioni passate al comando Web SDK. |
| `data.result` | Oggetto | Oggetto contenente il risultato del comando Web SDK. |

## `onCommandRejected` {#onCommandRejected}

Questa funzione di callback viene attivata prima che una promessa di comando venga rifiutata e contiene informazioni sul motivo per cui il comando è stato rifiutato. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.commandName` | Stringa | Nome del comando Web SDK eseguito. |
| `data.options` | Oggetto | Oggetto contenente le opzioni passate al comando Web SDK. |
| `data.error` | Oggetto | Oggetto contenente il messaggio di errore restituito dalla chiamata di rete del browser (`fetch` nella maggior parte dei casi) insieme al motivo per cui il comando è stato rifiutato. |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

Questa funzione di callback viene attivata prima dell&#39;esecuzione di una richiesta di rete. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.requestId` | Stringa | `requestId` generato da Web SDK per abilitare il debug. |
| `data.url` | Stringa | L’URL richiesto. |
| `data.payload` | Oggetto | Oggetto payload della richiesta di rete che verrà convertito in formato JSON e inviato nel corpo della richiesta tramite un metodo `POST`. |

## `onNetworkResponse` {#onNetworkResponse}

Questa funzione di callback viene attivata quando il browser riceve una risposta. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.requestId` | Stringa | `requestId` generato da Web SDK per abilitare il debug. |
| `data.url` | Stringa | L’URL richiesto. |
| `data.payload` | Oggetto | Oggetto payload che verrà convertito in formato JSON e inviato nel corpo della richiesta tramite un metodo `POST`. |
| `data.body` | Stringa | Il corpo della risposta in formato stringa. |
| `data.parsedBody` | Oggetto | Oggetto contenente il corpo della risposta analizzato. Se si verifica un errore durante l’analisi del corpo della risposta, questo parametro non è definito. |
| `data.status` | Stringa | Il codice di risposta in formato intero. |
| `data.retriesAttempted` | Intero | Numero di tentativi eseguiti durante l’invio della richiesta. Zero significa che la richiesta è riuscita al primo tentativo. |

## `onNetworkError` {#onNetworkError}

Questa funzione di callback viene attivata quando la richiesta di rete non riesce. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.requestId` | Stringa | `requestId` generato da Web SDK per abilitare il debug. |
| `data.url` | Stringa | L’URL richiesto. |
| `data.payload` | Oggetto | Oggetto payload che verrà convertito in formato JSON e inviato nel corpo della richiesta tramite un metodo `POST`. |
| `data.error` | Oggetto | Oggetto contenente il messaggio di errore restituito dalla chiamata di rete del browser (`fetch` nella maggior parte dei casi) insieme al motivo per cui il comando è stato rifiutato. |

## `onBeforeLog` {#onBeforeLog}

Questa funzione di callback viene attivata prima che l’SDK web registri qualsiasi elemento nella console. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.componentName` | Stringa | Nome del componente che ha generato il messaggio di registro. |
| `data.level` | Stringa | Livello di registrazione. Livelli supportati: `log`, `info`, `warn`, `error`. |
| `data.arguments` | Array di stringhe | Argomenti del messaggio di registro. |


## `onContentRendering` {#onContentRendering}

Questa funzione di callback viene attivata dal componente `personalization` in varie fasi del rendering. Il payload può variare a seconda del parametro `status`. Per informazioni dettagliate sui parametri della funzione, consulta l’esempio seguente.

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.componentName` | Stringa | Nome del componente che ha generato il messaggio di registro. |
| `data.payload` | Oggetto | Oggetto payload che verrà convertito in formato JSON e inviato nel corpo della richiesta tramite un metodo `POST`. |
| `data.status` | Stringa | Il componente `personalization` notifica all&#39;SDK Web lo stato del rendering.  Valori supportati: <ul><li>`rendering-started`: indica che Web SDK sta per eseguire il rendering delle proposte. Prima che l&#39;SDK Web inizi a eseguire il rendering di un ambito di decisione o di una visualizzazione, nell&#39;oggetto `data` è possibile visualizzare le proposte che stanno per essere sottoposte a rendering dal componente `personalization` e il nome dell&#39;ambito.</li><li>`no-offers`: indica che non è stato ricevuto alcun payload per i parametri richiesti.</li> <li>`rendering-failed`: indica che Web SDK non è riuscito a eseguire il rendering di una proposta.</li><li>`rendering-succeeded`: indica che il rendering è stato completato per un ambito di decisione.</li> <li>`rendering-redirect`: indica che Web SDK restituirà una proposta di reindirizzamento.</li></ul> |

## `onContentHiding` {#onContentHiding}

Questa funzione di callback viene attivata quando viene applicato o rimosso uno stile di pre-hiding.

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| Parametro | Tipo | Descrizione |
|---------|----------|----------|
| `data.instanceName` | Stringa | Il nome della variabile globale in cui è memorizzata l’istanza dell’SDK web. |
| `data.componentName` | Stringa | Nome del componente che ha generato il messaggio di registro. |
| `data.status` | Stringa | Il componente `personalization` notifica all&#39;SDK Web lo stato del rendering. Valori supportati: <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## Specificare gli hook di monitoraggio quando si utilizza il pacchetto NPM {#specify-monitoris-npm}

Se si utilizza Web SDK tramite il pacchetto [NPM](install/npm.md), è possibile specificare hook di monitoraggio nella funzione `createInstasnce`, come illustrato di seguito.

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## Esempio {#example}

Web SDK cerca un array di oggetti in una variabile globale denominata `__alloyMonitors`.

Per acquisire tutti gli eventi Web SDK, è necessario definire gli hook di monitoraggio prima che il codice Web SDK venga caricato sulla pagina. Ogni metodo di monitoraggio acquisisce un evento Web SDK.

Puoi definire gli hook di monitoraggio *dopo* il caricamento del codice Web SDK sulla pagina, ma gli hook attivati prima del caricamento della pagina *non* verranno acquisiti.

Quando definisci l’oggetto hook di monitoraggio, devi solo definire i metodi per i quali desideri definire una logica speciale.
Ad esempio, se ti interessa solo `onContentRendering`, puoi semplicemente definire tale metodo. Non è necessario utilizzare tutti gli hook di monitoraggio contemporaneamente.

È possibile definire più oggetti hook di monitoraggio. Tutti gli oggetti con il metodo specificato verranno chiamati quando viene attivato l&#39;evento corrispondente.

>[!TIP]
>
>Di seguito è riportata una pagina di esempio con tutti gli hook di monitoraggio implementati.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```
