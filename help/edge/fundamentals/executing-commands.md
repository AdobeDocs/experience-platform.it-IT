---
title: Esegui comandi Adobe Experience Platform Web SDK
description: Scopri come eseguire i comandi Experience Platform Web SDK
keywords: Esegui comandi;commandName;Promises;getLibraryInfo;oggetti di risposta;consenso;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# Esegui comandi


Dopo aver implementato il codice di base nella pagina web, puoi iniziare a eseguire i comandi con l&#39;SDK. Non è necessario attendere il file esterno (`alloy.js`) da caricare dal server prima di eseguire i comandi. Se il caricamento dell&#39;SDK non è stato completato, i comandi vengono messi in coda ed elaborati dall&#39;SDK il prima possibile.

I comandi vengono eseguiti utilizzando la seguente sintassi.

```javascript
alloy("commandName", options);
```

La `commandName` comunica all’SDK cosa fare, mentre `options` sono i parametri e i dati che si desidera trasmettere a un comando. Poiché le opzioni disponibili dipendono dal comando, consulta la documentazione per ulteriori dettagli su ciascun comando.

## Una nota sulle promesse

[Promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) sono fondamentali per la modalità di comunicazione dell’SDK con il codice presente nella pagina web. Una promessa è una struttura di programmazione comune e non è specifica per questo SDK o JavaScript. Una promessa funge da proxy per un valore non noto al momento della creazione della promessa. Una volta noto il valore, la promessa viene &quot;risolta&quot; con il valore . Le funzioni del gestore possono essere associate a una promessa, in modo che tu possa essere informato quando la promessa è stata risolta o quando si è verificato un errore nel processo di risoluzione della promessa. Per saperne di più sulle promesse, leggere [esercitazione](https://javascript.info/promise-basics) o qualsiasi altra risorsa sul web.

## Gestione del successo o dell’errore {#handling-success-or-failure}

Ogni volta che viene eseguito un comando, viene restituita una promessa. La promessa rappresenta l&#39;eventuale completamento del comando. Nell’esempio seguente, puoi utilizzare `then` e `catch` metodi per determinare quando il comando è riuscito o non è riuscito.

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

Se non è importante sapere quando il comando ha esito positivo, è possibile rimuovere la `then` chiama.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Allo stesso modo, se sapere quando il comando non riesce non è importante per te, puoi rimuovere il `catch` chiama.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Oggetti di risposta

Tutte le promesse restituite dai comandi vengono risolte con un `result` oggetto. L&#39;oggetto result conterrà i dati in base al comando e al consenso dell&#39;utente. Ad esempio, le informazioni sulla libreria vengono passate come proprietà dell&#39;oggetto results nel comando seguente.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Consenso

Se un utente non ha dato il proprio consenso per uno scopo particolare, la promessa sarà comunque risolta; tuttavia, l&#39;oggetto response conterrà solo le informazioni che possono essere fornite nel contesto di ciò a cui l&#39;utente ha acconsentito.
