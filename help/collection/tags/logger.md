---
title: logger
description: Invia informazioni alla console del browser durante il debug.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

L&#39;oggetto `_satellite.logger` contiene metodi che consentono di inviare messaggi di diagnostica o informativi alla console del browser quando è abilitato il [debug](../use-cases/debugging.md). Se il debug non è abilitato, tutte le chiamate al metodo `logger` non eseguono alcuna operazione.

Questi metodi consentono agli sviluppatori, ai tecnici addetti al marketing e ai tester di vedere facilmente quali attivatori si trovano all’interno di una proprietà tag e quando. Poiché questi messaggi della console vengono visualizzati solo quando è abilitato il debug, è possibile lasciare `logger` messaggi nelle distribuzioni in produzione senza influire sulla console del browser dei visitatori del sito.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Le versioni precedenti dell&#39;oggetto tag utilizzavano `_satellite.notify()`. La funzione `notify()` è obsoleta a favore di `_satellite.logger`.

## Metodi

Tutti i metodi `_satellite.logger` passano al metodo JavaScript `console.*` corrispondente quando è abilitato il debug. La maggior parte degli argomenti o oggetti `console` è supportata utilizzando `_satellite.logger`:

| Metodo | Inoltra a | Utilizzi consigliati |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Diagnostica dettagliata; alcuni browser potrebbero richiedere una registrazione dettagliata per visualizzarla. |
| `_satellite.logger.log()` | `console.log()` | Messaggi generali. |
| `_satellite.logger.info()` | `console.info()` | Eventi informativi di alto livello. |
| `_satellite.logger.warn()` | `console.warn()` | Problemi risolvibili. La voce della console è evidenziata in giallo. |
| `_satellite.logger.error()` | `console.error()` | Errori. La voce della console è evidenziata in rosso. Adobe consiglia di utilizzare `error` oggetti per gli stack. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Uscita console

In tutti i messaggi di output della console, la libreria precede quanto segue:

* **🚀**: consente di rilevare facilmente quali messaggi della console provengono dall&#39;implementazione del tag.
* **\[Origin\]**: nome della regola, dell&#39;azione, dell&#39;estensione o dell&#39;elemento dati da cui ha avuto origine il registro. Se si chiama un metodo logger all&#39;esterno dell&#39;implementazione (ad esempio tramite la console del browser), viene utilizzato `[Custom Script]`.
* **Output del messaggio**: l&#39;output del messaggio incluso quando si richiama il metodo.

>[!NOTE]
>
>I token di formattazione del browser come `%c`, `%s` e `%d` non vengono applicati a causa del logger che applica il prefisso `🚀 [Origin]`.
