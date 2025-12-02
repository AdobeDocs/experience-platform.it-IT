---
title: getLibraryInfo
description: Recuperare informazioni sulla versione corrente della libreria Web SDK.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# `getLibraryInfo`

Il comando `getLibraryInfo` fornisce informazioni sulla versione della libreria Web SDK attualmente utilizzata. È possibile utilizzare questo comando per tenere traccia delle versioni del Web SDK distribuite in proprietà Web diverse.

Eseguire il comando `getLibraryInfo` quando si chiama l&#39;istanza configurata del Web SDK. Questo comando viene in genere associato a una promessa JavaScript che consente di recuperare gli oggetti che popola.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`libraryInfo.commands`**: Array di comandi supportato da questa versione del Web SDK.
* **`libraryInfo.configs`**: array di impostazioni di configurazione supportato da questa versione del Web SDK.
* **`libraryInfo.version`**: versione della libreria Web SDK.

## Informazioni sulla libreria tramite l’estensione tag Web SDK

L’estensione tag non fornisce un’interfaccia per inviare questo comando. Utilizza l’editor di codice personalizzato seguendo la sintassi della libreria JavaScript.

Se si esegue questo comando utilizzando l&#39;estensione tag, verranno incluse sia la versione dell&#39;estensione tag che la versione della libreria, concatenate con il simbolo `+`. Viene elencata per prima la versione della libreria Web SDK, seguita dalla versione dell’estensione tag.
