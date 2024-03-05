---
title: getLibraryInfo
description: Recupera informazioni sulla versione corrente della libreria SDK Web.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# `getLibraryInfo`

Il `getLibraryInfo` Questo comando fornisce informazioni sulla versione della libreria SDK Web attualmente in uso. Puoi utilizzare questo comando per tenere traccia delle versioni dell’SDK web distribuite in diverse proprietà web.

## Informazioni sulla libreria tramite l’estensione tag Web SDK

L’estensione tag non fornisce un’interfaccia per inviare questo comando. Utilizza l’editor di codice personalizzato seguendo la sintassi della libreria JavaScript.

Se esegui questo comando utilizzando l’estensione tag, vengono incluse sia la versione dell’estensione tag che la versione della libreria, concatenate con un tag `+` simbolo. Viene elencata per prima la versione della libreria SDK Web, seguita dalla versione dell’estensione tag.

## Informazioni sulla libreria utilizzando la libreria JavaScript dell’SDK web

Esegui il `getLibraryInfo` quando si chiama l’istanza configurata dell’SDK per web. Questo comando viene in genere associato a una promessa JavaScript che consente di recuperare gli oggetti che popola.

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell’oggetto di risposta sono disponibili le seguenti proprietà:

* **`libraryInfo.commands`**: array di comandi supportato da questa versione dell’SDK web.
* **`libraryInfo.configs`**: array di impostazioni di configurazione supportato da questa versione dell’SDK web.
* **`libraryInfo.version`**: versione della libreria SDK web.
