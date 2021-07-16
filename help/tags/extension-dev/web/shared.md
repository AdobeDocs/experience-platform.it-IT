---
title: Moduli condivisi nelle estensioni web
description: Scopri come definire moduli di libreria condivisi per le estensioni web in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 78%

---

# Moduli condivisi nelle estensioni web

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta il seguente[documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo condiviso è un meccanismo mediante il quale è possibile comunicare con altre estensioni. Nelle implementazioni JavaScript, tutte le istanze dei moduli condivisi vengono create utilizzando il metodo [`getSharedModule`](../turbine.md#shared) fornito dalla variabile libera `turbine`.

Quando sviluppi la tua estensione di tag, puoi definire tutti i moduli condivisi che desideri che fornisca. Ad esempio, puoi creare un modulo che carica un ID utente in modo asincrono e quindi lo condivide con qualsiasi altra estensione tramite una [promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise), o promessa:

```javascript
var userIdPromise = new Promise(/* load user id, then resolve promise */);
module.exports = userIdPromise;
```

Nel [manifesto dell’estensione](../manifest.md) è necessario specificare il nome del modulo condiviso. Se gli si assegna il nome `user-id-promise`, un’altra estensione potrebbe quindi accedere al modulo condiviso nel modo seguente:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

È possibile usare come modulo condiviso qualsiasi elemento possa essere esportato da un modulo CommonJS (come funzioni, oggetti, stringhe, valori numerici o booleani).
