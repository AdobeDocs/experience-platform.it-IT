---
title: Recupero delle informazioni sulla libreria
seo-title: Recupero delle informazioni sulla libreria con Adobe Experience Platform Web SDK
description: Scoprite come recuperare informazioni sulla libreria caricata nel sito Web
seo-description: Scopri come recuperare informazioni sulla libreria caricata nel sito Web dall’SDK di Adobe Experience Cloud, che viene raccolta automaticamente
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Recupero delle informazioni sulla libreria

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Spesso è utile accedere ad alcuni dei dettagli della libreria caricata sul sito Web. A questo scopo, eseguite il `getLibraryInfo` comando come segue:

```js
alloy("getLibraryInfo").then(function(libraryInfo) {
  console.log(libraryInfo.version);
});
```

Attualmente, l&#39; `libraryInfo` oggetto fornito contiene le proprietà seguenti:

* `version` Questa è la versione della libreria caricata. Ad esempio, se la versione della libreria caricata fosse 1.0.0, il valore sarebbe `1.0.0`.