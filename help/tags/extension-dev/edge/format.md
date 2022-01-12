---
title: Moduli libreria nelle estensioni Edge
description: Formatta i moduli della libreria per le estensioni di tag in una proprietà edge.
exl-id: 82b98972-6fa2-4143-bcf4-c5dac1ca0e7f
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 92%

---

# Moduli libreria nelle estensioni Edge

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

>[!IMPORTANT]
>
>Questo documento descrive il formato del modulo libreria per le estensioni Edge. Se stai sviluppando un’estensione web, consulta la guida sulla [formattazione dei moduli di estensione web](../web/format.md).

Un modulo libreria è un codice riutilizzabile fornito da un’estensione ed emesso all’interno della libreria di tag runtime di Adobe Experience Platform (libreria che viene eseguita sul nodo edge). Ad esempio, un tipo di azione `sendBeacon` avrà un modulo libreria che verrà eseguito sul nodo Edge e invierà un beacon.

Il modulo libreria è strutturato come [modulo CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules). In un modulo CommonJS, sono disponibili le seguenti variabili:

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
