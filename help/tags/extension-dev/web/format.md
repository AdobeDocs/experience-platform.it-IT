---
title: Moduli libreria nelle estensioni Web
description: Scopri come formattare i moduli libreria per le estensioni Web in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 77%

---

# Moduli libreria nelle estensioni web

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta il seguente[documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

>[!IMPORTANT]
>
>Questo documento descrive il formato dei moduli libreria per le estensioni web. Se stai sviluppando un’estensione Edge, consulta invece la guida sulla [formattazione dei moduli per estensioni Edge](../edge/format.md).

Un modulo libreria è un pezzo di codice riutilizzabile fornito da un&#39;estensione che viene emessa all&#39;interno della libreria di runtime di tag in Adobe Experience Platform. Questa libreria viene quindi eseguita sul sito web del client. Ad esempio, un tipo di evento `gesture` avrà un modulo libreria che verrà eseguito sul sito web del client e rileverà i movimenti dell’utente.

Il modulo libreria è strutturato come [modulo CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1.1). In un modulo CommonJS, sono disponibili le seguenti variabili:

## [!DNL require]

È disponibile una funzione `require` che consente di accedere a:

1. Moduli di base forniti dai tag. È possibile accedere a questi moduli utilizzando `require('@adobe/reactor-name-of-module')`. Per ulteriori informazioni, consulta il documento sui [moduli core](./core.md) disponibili.
1. Altri moduli all’interno dell’estensione. È possibile accedere a qualsiasi modulo dell’estensione tramite il relativo percorso. Il percorso relativo deve iniziare con `./` oppure `../`.

Esempio di utilizzo:

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
```

## [!DNL module]

È disponibile una variabile gratuita denominata `module` che consente di esportare l’API del modulo.

Esempio di utilizzo:

```javascript
module.exports = function(…) { … }
```

## [!DNL exports]

È disponibile una variabile gratuita denominata `exports` che consente di esportare l’API del modulo.

Esempio di utilizzo:

```javascript
exports.sayHello = function(…) { … }
```

Si tratta di un’alternativa a `module.exports`, ma il suo utilizzo è più limitato. Consulta [Informazioni su “module.exports” ed “exports” in node.js](https://www.sitepoint.com/understanding-module-exports-exports-node-js/) per una comprendere meglio le differenze tra `module.exports` e `exports` e le relative avvertenze sull’utilizzo di `exports`. In caso di dubbi, utilizza `module.exports` anziché `exports`.

## Esecuzione e caching

Quando la libreria di runtime di tag viene eseguita, i moduli verranno immediatamente &quot;installati&quot; e le loro esportazioni sono memorizzate nella cache. Nel seguente modulo di esempio:

```javascript
console.log('runs on startup');

module.exports = function(settings) {
  console.log('runs when necessary');
}
```

`runs on startup` verranno registrati immediatamente, mentre  `runs when necessary` verranno registrati solo una volta che la funzione esportata viene chiamata dal motore di tag. Anche se potrebbe non essere necessario per lo scopo del modulo, è possibile trarne vantaggio eseguendo eventuali configurazioni necessarie prima di esportare la funzione.
