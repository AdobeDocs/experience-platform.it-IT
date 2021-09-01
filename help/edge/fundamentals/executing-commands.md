---
title: Esegui comandi Adobe Experience Platform Web SDK
description: Scopri come eseguire i comandi Experience Platform Web SDK
keywords: Esegui comandi;commandName;Promises;getLibraryInfo;oggetti di risposta;consenso;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ca3ee230d510dfb9de400b6f573a612ec33c8f7a
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# Esegui comandi


Dopo aver implementato il codice di base nella pagina web, puoi iniziare a eseguire i comandi con l&#39;SDK. Non è necessario attendere che il file esterno (`alloy.js`) venga caricato dal server prima di eseguire i comandi. Se il caricamento dell&#39;SDK non è stato completato, i comandi vengono messi in coda ed elaborati dall&#39;SDK il prima possibile.

I comandi vengono eseguiti utilizzando la seguente sintassi.

```javascript
alloy("commandName", options);
```

Il `commandName` indica all&#39;SDK cosa fare, mentre `options` sono i parametri e i dati che desideri trasmettere a un comando. Poiché le opzioni disponibili dipendono dal comando, consulta la documentazione per ulteriori dettagli su ciascun comando.

## Una nota sulle promesse

[](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) Le promesse sono fondamentali per il modo in cui l’SDK comunica con il codice sulla tua pagina web. Una promessa è una struttura di programmazione comune e non è specifica per questo SDK o JavaScript. Una promessa funge da proxy per un valore non noto al momento della creazione della promessa. Una volta noto il valore, la promessa viene &quot;risolta&quot; con il valore . Le funzioni del gestore possono essere associate a una promessa, in modo che tu possa essere informato quando la promessa è stata risolta o quando si è verificato un errore nel processo di risoluzione della promessa. Per ulteriori informazioni sulle promesse, leggi [questa esercitazione](https://javascript.info/promise-basics) o una delle altre risorse sul web.

## Gestione del successo o dell’errore {#handling-success-or-failure}

Ogni volta che viene eseguito un comando, viene restituita una promessa. La promessa rappresenta l&#39;eventuale completamento del comando. Nell&#39;esempio seguente, è possibile utilizzare i metodi `then` e `catch` per determinare quando il comando ha avuto esito positivo o negativo.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Se sapere quando il comando ha esito positivo non è importante, puoi rimuovere la chiamata `then` .

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Allo stesso modo, se sapere quando il comando non riesce non è importante per te, puoi rimuovere la chiamata `catch` .

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Oggetti di risposta

Tutte le promesse restituite dai comandi vengono risolte con un oggetto `result`. L&#39;oggetto result conterrà i dati in base al comando e al consenso dell&#39;utente. Ad esempio, le informazioni sulla libreria vengono passate come proprietà dell&#39;oggetto results nel comando seguente.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
  });
```

### Consenso

Se un utente non ha dato il proprio consenso per uno scopo particolare, la promessa sarà comunque risolta; tuttavia, l&#39;oggetto response conterrà solo le informazioni che possono essere fornite nel contesto di ciò a cui l&#39;utente ha acconsentito.
