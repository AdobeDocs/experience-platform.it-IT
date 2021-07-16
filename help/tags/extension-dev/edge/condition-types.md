---
title: Tipi di condizioni per le estensioni Edge
description: Scopri come definire un modulo libreria per tipi di condizione per un’estensione Edge in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 63%

---

# Tipi di condizioni per le estensioni Edge

>[!NOTE]
>
> Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo di libreria di tipo condizione valuta se qualcosa è vero o falso e restituisce un valore booleano.

>[!IMPORTANT]
>
>Questo documento descrive i tipi di condizioni per le estensioni edge. Se stai sviluppando un&#39;estensione web, consulta la guida sui [tipi di condizioni per le estensioni web](../web/condition-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

Ad esempio, se desideri valutare se l&#39;utente si trova sull&#39;host `example.com`, il modulo potrebbe avere questo aspetto.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Se si desidera rendere il nome host configurabile dall&#39;utente per consentire l&#39;input di un nome host e salvarlo nell&#39;oggetto settings, l&#39;oggetto potrebbe avere un aspetto simile a questo esempio.

```js
{
  "hostname": "example.com"
}
```

Per utilizzare il nome dell’host definito dall’utente, è necessario modificare il modulo come segue:

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## Risultato condizione

Il risultato restituito da un modulo condizione può essere uno dei seguenti:

1. Un valore booleano (`true` o `false`).
1. Una [promessa](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) che restituisce un valore booleano una volta risolta.

## Contesto del modulo Libreria

Tutti i moduli delle condizioni hanno accesso a una variabile `context` fornita quando viene chiamato il modulo. Per saperne di più [fai clic qui](./context.md).
