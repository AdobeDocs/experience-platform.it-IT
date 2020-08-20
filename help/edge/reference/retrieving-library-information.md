---
title: Recupero delle informazioni sulla libreria
seo-title: Recupero delle informazioni sulla libreria con Adobe Experience Platform Web SDK
description: Scoprite come recuperare informazioni sulla libreria caricata nel sito Web
seo-description: Scopri come recuperare informazioni sulla libreria caricata nel sito Web da Adobe Experience Cloud SDK raccoglie automaticamente
keywords: library; library information;getLibraryInfo;libraryInfo;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
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