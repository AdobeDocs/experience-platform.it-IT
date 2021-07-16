---
title: Moduli libreria nelle estensioni Edge
description: Formatta i moduli della libreria per le estensioni di tag in una proprietà edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 81%

---

# Moduli libreria nelle estensioni Edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

>[!IMPORTANT]
>
>Questo documento descrive il formato del modulo libreria per le estensioni Edge. Se stai sviluppando un’estensione web, consulta la guida sulla [formattazione dei moduli di estensione web](../web/format.md).

Un modulo libreria è un pezzo di codice riutilizzabile fornito da un&#39;estensione che viene emessa all&#39;interno della libreria di runtime di tag in Adobe Experience Platform (la libreria che viene eseguita sul nodo Edge). Ad esempio, un tipo di azione `sendBeacon` avrà un modulo libreria che verrà eseguito sul nodo Edge e invierà un beacon.

Il modulo libreria è strutturato come [modulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). In un modulo CommonJS, sono disponibili le seguenti variabili:

## [!DNL require]

È disponibile una funzione `require` per accedere ai moduli all’interno dell’estensione. È possibile accedere a qualsiasi modulo dell’estensione tramite il relativo percorso. Il percorso relativo deve iniziare con `./` oppure `../`.

Esempio di utilizzo:

```js
var transformHelper = require('../helpers/transform');
transformHelper.execute({a: 'b'});
```

## [!DNL module]

È disponibile una variabile gratuita denominata `module` che consente di esportare l’API del modulo.

Esempio di utilizzo:

```js
module.exports = (…) => { … }
```

## [!DNL exports]

È disponibile una variabile gratuita denominata `exports` che consente di esportare l’API del modulo.

Esempio di utilizzo:

```js
exports.sayHello = (…) => { … }
```

Si tratta di un’alternativa a `module.exports`, ma il suo utilizzo è più limitato. Consulta [Informazioni su “module.exports” ed “exports” in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) per una comprendere meglio le differenze tra `module.exports` e `exports` e le relative avvertenze sull’utilizzo di `exports`. In caso di dubbi, utilizza `module.exports` anziché `exports`.

## Firma del modulo del lato server

Tutti i tipi di modulo (elementi di dati, condizioni o azioni) forniti dall’estensione verranno chiamati con gli stessi parametri: [context](./context.md).

```js
exports.sayHello = (context) => { … }
```
