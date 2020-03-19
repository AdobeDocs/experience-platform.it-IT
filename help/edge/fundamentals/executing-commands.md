---
title: Esecuzione di comandi
seo-title: Esecuzione di comandi SDK Web per Adobe Experience Platform
description: Scopri come eseguire i comandi SDK Web della piattaforma Experience
seo-description: Scopri come eseguire i comandi SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Esecuzione di comandi

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Dopo che il codice di base è stato implementato nella pagina Web, puoi iniziare a eseguire i comandi con l’SDK. Non è necessario attendere che il file esterno \(`alloy.js`\) venga caricato dal server prima di eseguire i comandi. Se l’SDK non ha completato il caricamento, i comandi vengono messi in coda ed elaborati dall’SDK il prima possibile.

I comandi vengono eseguiti utilizzando la sintassi seguente.

```javascript
alloy("commandName", options);
```

L’ `commandName` SDK spiega all’SDK cosa fare, mentre `options` sono i parametri e i dati da trasmettere a un comando. Poiché le opzioni disponibili dipendono dal comando, consultare la documentazione per ulteriori dettagli su ciascun comando.

## Una nota sulle promesse

[Le promesse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) sono fondamentali per il modo in cui l’SDK comunica con il codice sulla tua pagina Web. Una promessa è una struttura di programmazione comune e non è specifica per questo SDK o JavaScript. Una promessa funge da proxy per un valore non noto al momento della creazione della promessa. Una volta noto il valore, la promessa viene &quot;risolta&quot; con il valore. Le funzioni del gestore possono essere associate a una promessa, in modo che sia possibile ricevere una notifica quando la promessa è stata risolta o quando si è verificato un errore nel processo di risoluzione della promessa. Per saperne di più sulle promesse, leggete [questa esercitazione](https://javascript.info/promise-basics) o una delle altre risorse disponibili sul Web.

## Gestione del successo o del fallimento

Ogni volta che viene eseguito un comando, viene restituita una promessa. La promessa rappresenta il completamento finale del comando. Nell&#39;esempio seguente, è possibile utilizzare `then` e `catch` metodi per determinare se il comando ha avuto esito positivo o negativo.

```javascript
alloy("commandName", options)
  .then(function(value) {
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
  .then(function(value) {
    // The command succeeded.
    // "value" will be whatever the command returned
  })
```

## Eliminazione degli errori

Se la promessa viene rifiutata e non hai aggiunto una `catch` chiamata, l’errore &quot;bubbles up&quot; viene visualizzato nella console sviluppatore del browser, indipendentemente dal fatto che la registrazione sia abilitata o meno nell’SDK Web di Adobe Experience Platform. Se questo è un problema, puoi impostare l’opzione di `suppressErrors` configurazione su `true` come descritto in [Configurazione dell’SDK](configuring-the-sdk.md).
