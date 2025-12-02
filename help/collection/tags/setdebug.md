---
title: setDebug()
description: Abilita il debug sul sito tramite la console del browser.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

Il metodo `_satellite.setDebug()` ti consente di abilitare o disabilitare il [debug](../use-cases/debugging.md) sul tuo sito. Questo metodo è destinato all’esecuzione locale nella console del browser; Adobe consiglia di non chiamare questo metodo all’interno delle regole dei tag.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: abilita il [debug](../use-cases/debugging.md). I messaggi generati dalla libreria di tag (incluso [`_satellite.logger`](logger.md)) sono visibili nella console del browser.
* **`_satellite.setDebug(false);`**: disabilita il debug. I messaggi della console generati dalla libreria di tag non sono visibili.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>I messaggi scritti con l&#39;elemento nativo `console.log()` di JavaScript sono sempre visibili a chiunque abbia DevTools aperto. Adobe consiglia di utilizzare [`_satellite.logger`](logger.md) ove possibile.

## Persistenza modalità debug

Quando si chiama questo metodo, la modalità di debug utilizza l&#39;ambito seguente:

* **Sessione browser**: la modalità di debug persiste nei vari caricamenti di pagina. L’opzione rimane attiva finché non terminate la sessione del browser o non la disattivate esplicitamente.
* **Ambito di origine**: la modalità di debug persiste solo per lo stesso sito (dominio + porta + protocollo).
* **Per profilo browser**: la modalità di debug non è cross-profile.

Altre forme di [debug](../use-cases/debugging.md) possono influire sulla modalità di debug e sovrascriverla utilizzando il metodo della console del browser.
