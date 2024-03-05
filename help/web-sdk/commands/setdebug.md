---
title: setDebug
description: Abilita o disabilita l'impostazione di debug di Web SDK.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Il `setDebug` consente di entrare o uscire dalla modalità di debug in Web SDK. È una delle diverse opzioni disponibili per [debug](../use-cases/debugging.md). L’Adobe consiglia di abilitare la modalità di debug all’interno degli ambienti di sviluppo o solo sul computer locale all’interno degli ambienti di produzione.

## Impostare il debug utilizzando l’estensione tag Web SDK

L’estensione tag non consente di attivare/disattivare le opzioni di debug nell’interfaccia utente. Puoi utilizzare l’editor di codice personalizzato utilizzando la sintassi JavaScript oppure immettere il codice JavaScript nella console del browser mentre sei sul sito.

## Impostare il debug utilizzando la libreria JavaScript dell’SDK per web

Esegui il `setDebug` quando si chiama l’istanza configurata dell’SDK per web. L’unica opzione nell’oggetto di configurazione è `enabled`, valore booleano che determina se la modalità di debug è abilitata.

```js
alloy("setDebug", {"enabled": true});
```
