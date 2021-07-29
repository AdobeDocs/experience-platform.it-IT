---
title: Moduli condivisi nelle estensioni web
description: Scopri come definire moduli di libreria condivisi per le estensioni web in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 65%

---

# Moduli condivisi nelle estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta il seguente[documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo condiviso è un meccanismo mediante il quale è possibile comunicare con altre estensioni. Ad esempio, l’estensione A può caricare una parte di dati in modo asincrono e renderla disponibile all’estensione B tramite una [promise](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise), o promessa.

Nelle implementazioni JavaScript, tutte le istanze dei moduli condivisi vengono create utilizzando il metodo [`getSharedModule`](../turbine.md#shared) fornito dalla variabile libera `turbine`.

I moduli condivisi sono inclusi nelle librerie di tag anche quando non vengono mai chiamati da altre estensioni. Per non aumentare inutilmente la dimensione della libreria, occorre prestare attenzione a ciò che viene esposto come modulo condiviso.

I moduli condivisi non hanno un componente vista.

Quando sviluppi la tua estensione di tag, puoi definire tutti i moduli condivisi che desideri che fornisca. Ad esempio, puoi creare un modulo che carica un ID utente in modo asincrono e quindi lo condivide con qualsiasi altra estensione tramite una promise, o promessa:

```javascript
var userIdPromise = new Promise(/* load user ID, then resolve promise */);
module.exports = userIdPromise;
```

Nel [manifesto estensione](../manifest.md), devi fornire un nome per questo modulo condiviso. Se gli si assegna il nome `user-id-promise`, un’altra estensione potrebbe quindi accedere al modulo condiviso nel modo seguente:

```javascript
var userIdPromise = turbine.getSharedModule('user-extension', 'user-id-promise');
```

È possibile usare come modulo condiviso qualsiasi elemento possa essere esportato da un modulo CommonJS (come funzioni, oggetti, stringhe, valori numerici o booleani).
