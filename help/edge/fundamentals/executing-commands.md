---
title: Esecuzione di comandi
seo-title: Esecuzione di comandi Adobe Experience Platform Web SDK
description: Scopri come eseguire  comandi SDK Web per Experienci Platform
seo-description: Scopri come eseguire  comandi SDK Web per Experienci Platform
translation-type: tm+mt
source-git-commit: bf4194e1449bddd662f2152f84dbbe90060b5d30
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---


# Esecuzione di comandi

Dopo che il codice di base è stato implementato nella pagina Web, puoi iniziare a eseguire i comandi con l’SDK. Non è necessario attendere che il file esterno \(`alloy.js`\) venga caricato dal server prima di eseguire i comandi. Se l’SDK non ha completato il caricamento, i comandi vengono messi in coda ed elaborati dall’SDK il prima possibile.

I comandi vengono eseguiti utilizzando la sintassi seguente.

```javascript
alloy("commandName", options);
```

L’ `commandName` SDK spiega all’SDK cosa fare, mentre `options` sono i parametri e i dati da trasmettere a un comando. Poiché le opzioni disponibili dipendono dal comando, consultare la documentazione per ulteriori dettagli su ciascun comando.

## Una nota sulle promesse

[Le promesse](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) sono fondamentali per il modo in cui l’SDK comunica con il codice sulla tua pagina Web. Una promessa è una struttura di programmazione comune e non è specifica per questo SDK o JavaScript. Una promessa funge da proxy per un valore non noto al momento della creazione della promessa. Una volta noto il valore, la promessa viene &quot;risolta&quot; con il valore. Le funzioni del gestore possono essere associate a una promessa, in modo che sia possibile ricevere una notifica quando la promessa è stata risolta o quando si è verificato un errore nel processo di risoluzione della promessa. Per saperne di più sulle promesse, leggete [questa esercitazione](https://javascript.info/promise-basics) o una delle altre risorse disponibili sul Web.

## Gestione del successo o del fallimento {#handling-success-or-failure}

Ogni volta che viene eseguito un comando, viene restituita una promessa. La promessa rappresenta il completamento finale del comando. Nell&#39;esempio seguente, è possibile utilizzare `then` e `catch` metodi per determinare se il comando ha avuto esito positivo o negativo.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Se sapere quando il comando ha esito positivo non è importante, puoi rimuovere la `then` chiamata.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  })
```

Allo stesso modo, se sapere quando il comando non riesce non è importante per voi, potete rimuovere la `catch` chiamata.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

### Oggetti di risposta

Tutte le promesse restituite dai comandi vengono risolte con un `result` oggetto. L&#39;oggetto result conterrà i dati in base al comando e al consenso dell&#39;utente. Ad esempio, le informazioni sulla libreria vengono trasmesse come proprietà dell&#39;oggetto result nel comando seguente.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(results.libraryInfo.version);
});
```

### Consenso

Se un utente non ha dato il proprio consenso per uno scopo particolare, la promessa sarà ancora risolta; tuttavia, l&#39;oggetto response conterrà solo le informazioni che possono essere fornite nel contesto a cui l&#39;utente ha acconsentito.
