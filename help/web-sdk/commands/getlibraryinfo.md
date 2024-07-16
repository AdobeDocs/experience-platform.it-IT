---
title: getLibraryInfo
description: Recupera informazioni sulla versione corrente della libreria SDK Web.
exl-id: f2bc0185-71c9-4d77-b9d2-b777a41a20e5
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

Il comando `getLibraryInfo` fornisce informazioni sulla versione della libreria SDK Web attualmente utilizzata. Puoi utilizzare questo comando per tenere traccia delle versioni dell’SDK web distribuite in diverse proprietà web.

## Informazioni sulla libreria tramite l’estensione tag Web SDK

L’estensione tag non fornisce un’interfaccia per inviare questo comando. Utilizza l’editor di codice personalizzato seguendo la sintassi della libreria JavaScript.

Se si esegue questo comando utilizzando l&#39;estensione tag, verranno incluse sia la versione dell&#39;estensione tag che la versione della libreria, concatenate con il simbolo `+`. Viene elencata per prima la versione della libreria SDK Web, seguita dalla versione dell’estensione tag.

## Informazioni sulla libreria utilizzando la libreria JavaScript dell’SDK per web

Esegui il comando `getLibraryInfo` quando chiami l&#39;istanza configurata dell&#39;SDK Web. Questo comando viene in genere associato a una promessa JavaScript che consente di recuperare gli oggetti che popola.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`libraryInfo.commands`**: Array di comandi supportato da questa versione dell&#39;SDK Web.
* **`libraryInfo.configs`**: array di impostazioni di configurazione supportato da questa versione dell&#39;SDK Web.
* **`libraryInfo.version`**: versione della libreria Web SDK.
