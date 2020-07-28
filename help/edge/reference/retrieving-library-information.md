---
title: Recupero delle informazioni sulla libreria
seo-title: Recupero delle informazioni sulla libreria con  Adobe Experience Platform Web SDK
description: Scoprite come recuperare informazioni sulla libreria caricata nel sito Web
seo-description: Scopri come recuperare informazioni sulla libreria caricata nel sito Web da Adobe Experience Cloud SDK raccoglie automaticamente
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Recupero delle informazioni sulla libreria

Spesso è utile accedere ad alcuni dei dettagli della libreria caricata sul sito Web. A questo scopo, eseguite il `getLibraryInfo` comando come segue:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Attualmente, l&#39; `libraryInfo` oggetto fornito contiene le proprietà seguenti:

* `version` Questa è la versione della libreria caricata. Ad esempio, se la versione della libreria caricata fosse 1.0.0, il valore sarebbe `1.0.0`.