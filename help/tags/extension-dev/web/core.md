---
title: Moduli libreria Core per le estensioni Web
description: Scopri i moduli libreria di base che puoi utilizzare con le estensioni web.
exl-id: 7fb63208-aed0-4add-b6da-8e4aea063d0a
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 93%

---

# Moduli libreria Core per le estensioni Web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [document](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Questo documento fornisce un elenco dei moduli libreria Coredi che è possibile utilizzare nelle estensioni Web. Per accedere a questi moduli, utilizza `require('@adobe/{MODULE}')`, dove `{MODULE}` è il nome del modulo principale che desideri utilizzare.

## [!DNL reactor-object-assign]

`reactor-object-assign` imita il metodo nativo [`Object.assign`](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) copiando le proprietà dagli oggetti sorgente a un oggetto target.

```javascript
var objectAssign = require('@adobe/reactor-object-assign');
var all = objectAssign({ a: 'a' }, { b: 'b' });
```

## [!DNL reactor-cookie]

L’oggetto `reactor-cookie` è un’utility per la lettura e la scrittura di cookie. Per ulteriori informazioni, vedi il [pacchetto npm js-cookie](https://www.npmjs.com/package/js-cookie).

```javascript
var cookie = require('@adobe/reactor-cookie');
cookie.set('foo', 'bar');
console.log(cookie.get('foo'));
cookie.remove('foo');
```

### [!DNL reactor-document]

`reactor-document` rappresenta l’oggetto [`Document`](https://developer.mozilla.org/it-IT/docs/Web/API/Document). Questo può essere utile quando si esegue il test del modulo consentendo ai test di inserire un oggetto fittizio `document` utilizzando utility come [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var document = require('@adobe/reactor-document');
console.log(document.location);
```

### [!DNL reactor-query-string]

`reactor-query-string` è un’utility per effettuare il parsing e la serializzazione delle [stringhe di query](https://developer.mozilla.org/en-US/docs/Web/API/HTMLHyperlinkElementUtils/search).

```javascript
var queryString = require('@adobe/reactor-query-string');
var parsed = queryString.parse(location.search);
console.log(parsed.campaign);
var obj = {
  campaign: 'Campaign A'
};
var stringified = queryString.stringify(obj);
```

Per questa utility sono disponibili i seguenti metodi:

* `queryString.parse({STRING})`: effettua il parsing di una stringa di query in un oggetto. I caratteri iniziali `?`, `#` e `&` nella stringa di query vengono ignorati.
* `queryString.stringify({OBJECT})`: converte un oggetto in una stringa di query.

### [!DNL reactor-load-script]

`reactor-load-script` è una funzione che carica uno script quando viene fornito un URL. Un tag script verrà creato e posizionato all’interno del nodo `head` del documento. Verrà restituita una [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) da utilizzare per determinare quando il caricamento dello script ha esito positivo o negativo.

```javascript
var loadScript = require('@adobe/reactor-load-script');
var url = 'http://code.jquery.com/jquery-3.1.1.js';
loadScript(url).then(function() {
  // Do something ...
})
```

### [!DNL reactor-promise]

`reactor-promise` è un costruttore che imita l’[API Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) nativa di ECMAScript 6. Se è disponibile l’API Promise nativa, verrà restituita quest’ultima.

```javascript
var Promise = require('@adobe/reactor-promise');
new Promise(function(resolve) {
  resolve();
}, function(err) {
  console.error(err);
});
```

### [!DNL reactor-window]

`reactor-window` rappresenta l’oggetto [`Window`](https://developer.mozilla.org/it-IT/docs/Web/API/Window). Questo può essere utile quando si esegue il test del modulo consentendo ai test di inserire un oggetto fittizio `Window` utilizzando utility come [`inject-loader`](https://www.npmjs.com/package/inject-loader).

```javascript
var window = require('@adobe/reactor-window');
console.log(window.document);
```
