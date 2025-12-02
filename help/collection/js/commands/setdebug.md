---
title: setDebug
description: Attiva o disattiva l'impostazione di debug di Web SDK.
exl-id: 9faac147-b7c7-4732-8454-35102970dae0
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# `setDebug`

Il comando `setDebug` consente di entrare o uscire dalla modalità di debug in Web SDK. Si tratta di una delle diverse opzioni disponibili per il [debug](../../use-cases/debugging.md). Adobe consiglia di abilitare la modalità di debug all’interno degli ambienti di sviluppo o solo sul computer locale all’interno degli ambienti di produzione.

Eseguire il comando `setDebug` quando si chiama l&#39;istanza configurata del Web SDK. L&#39;unica opzione nell&#39;oggetto di configurazione è `enabled`, un valore booleano che determina se la modalità di debug è abilitata.

```js
alloy("setDebug", {"enabled": true});
```

## Impostare il debug utilizzando l&#39;estensione tag Web SDK

Chiamare [`_satellite.setDebug()`](/help/collection/tags/setdebug.md) nella console del browser in una pagina in cui è implementata una libreria di tag. L’estensione tag Web SDK non consente di attivare o disattivare le opzioni di debug nell’interfaccia utente dei tag.
