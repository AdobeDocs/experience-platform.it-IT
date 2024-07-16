---
title: setDebug
description: Abilita o disabilita l'impostazione di debug di Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# `setDebug`

Il comando `setDebug` consente di entrare o uscire dalla modalità di debug in Web SDK. Si tratta di una delle diverse opzioni disponibili per il [debug](../use-cases/debugging.md). L’Adobe consiglia di abilitare la modalità di debug all’interno degli ambienti di sviluppo o solo sul computer locale all’interno degli ambienti di produzione.

## Impostare il debug utilizzando l’estensione tag Web SDK

L’estensione tag non consente di attivare/disattivare le opzioni di debug nell’interfaccia utente. Puoi utilizzare l’editor di codice personalizzato utilizzando la sintassi JavaScript oppure immettere il codice JavaScript nella console del browser mentre sei sul sito.

## Impostare il debug utilizzando la libreria Web SDK JavaScript

Esegui il comando `setDebug` quando chiami l&#39;istanza configurata dell&#39;SDK Web. L&#39;unica opzione nell&#39;oggetto di configurazione è `enabled`, un valore booleano che determina se la modalità di debug è abilitata.

```js
alloy("setDebug", {"enabled": true});
```
