---
title: Eseguire i comandi di Adobe Experience Platform Web SDK
description: Scopri come eseguire i comandi Experienci Platform Web SDK
keywords: Eseguire comandi;nomeComando;Promesse;getLibraryInfo;oggetti di risposta;consenso;
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: ffc60e83285188bc5b0f6eb7a20fafee16d51d4d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Esegui comandi


Una volta implementato il codice di base nella pagina web, puoi iniziare a eseguire comandi con l’SDK. Non è necessario attendere il file esterno (`alloy.js`) da caricare dal server prima di eseguire i comandi. Se l&#39;SDK non ha terminato il caricamento, i comandi vengono messi in coda ed elaborati dall&#39;SDK il prima possibile.

I comandi vengono eseguiti utilizzando la seguente sintassi.

```javascript
alloy("commandName", options);
```

Il `commandName` indica all’SDK cosa fare, mentre `options` sono i parametri e i dati che desideri trasmettere a un comando. Poiché le opzioni disponibili dipendono dal comando, consulta la documentazione per maggiori dettagli su ciascun comando.

## Una nota sulle promesse

[Promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) sono fondamentali per la comunicazione dell&#39;SDK con il codice sulla pagina web. Una promessa è una struttura di programmazione comune e non è specifica per questo SDK o anche per JavaScript. Una promise funge da proxy per un valore che non è noto al momento della creazione della promise. Una volta che il valore è noto, la promessa viene &quot;risolta&quot; con il valore. Le funzioni del gestore possono essere associate a una promessa, in modo da poter ricevere una notifica quando la promessa è stata risolta o quando si è verificato un errore nel processo di risoluzione della promessa. Per ulteriori informazioni sulle promesse, leggere [questa esercitazione](https://javascript.info/promise-basics) o da una qualsiasi delle altre risorse del web.

## Gestione di operazioni riuscite o non riuscite {#handling-success-or-failure}

Ogni volta che viene eseguito un comando, viene restituita una promessa. La promessa rappresenta il completamento finale del comando. Nell’esempio seguente, puoi utilizzare `then` e `catch` metodi per determinare quando il comando è riuscito o non è riuscito.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "result" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Se non è importante sapere quando il comando viene eseguito correttamente, è possibile rimuovere `then` chiamare.

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

Allo stesso modo, se non è importante sapere quando il comando ha esito negativo, è possibile rimuovere `catch` chiamare.

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### Oggetti di risposta

Tutte le promesse restituite dai comandi vengono risolte con un `result` oggetto. L’oggetto risultato conterrà i dati in base al comando e al consenso dell’utente. Ad esempio, le informazioni della libreria vengono passate come proprietà dell&#39;oggetto results nel comando seguente.

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### Consenso

Se un utente non ha dato il proprio consenso per uno scopo particolare, la promessa verrà comunque risolta; tuttavia, l’oggetto di risposta conterrà solo le informazioni che possono essere fornite nel contesto di ciò a cui l’utente ha acconsentito.
