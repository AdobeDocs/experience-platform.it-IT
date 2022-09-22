---
title: Tipi di condizioni per le estensioni Edge
description: Scopri come definire un modulo libreria per tipi di condizione per un’estensione Edge in Adobe Experience Platform.
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 69%

---

# Tipi di condizioni per le estensioni Edge

>[!NOTE]
>
> Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In una regola di tag, una condizione viene valutata dopo che si è verificato un evento. Tutte le condizioni devono restituire true affinché la regola possa continuare l’elaborazione. I tipi di condizione vengono forniti dalle estensioni e valutano se qualcosa è vero o falso e restituisce un valore booleano.

Ad esempio, un’estensione potrebbe fornire un tipo di condizione “viewport contains” in cui l’utente di potrebbe specificare un selettore CSS. Quando la condizione viene valutata sul sito web del client, l’estensione sarà in grado di trovare elementi che corrispondono al selettore CSS e restituire se uno di essi è contenuto nella finestra dell’utente.

Questo documento illustra come definire i tipi di condizioni per un&#39;estensione Edge in Adobe Experience Platform.

>[!IMPORTANT]
>
>Se stai sviluppando un&#39;estensione web, consulta la guida sui [tipi di condizioni per le estensioni web](../web/condition-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli di libreria e con il modo in cui sono integrati nelle estensioni edge. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di condizione sono in genere costituiti dai seguenti elementi:

1. Visualizzazione nell’interfaccia utente di Raccolta dati che consente agli utenti di modificare le impostazioni della condizione.
2. Un modulo libreria emesso all&#39;interno della libreria di runtime di tag per interpretare le impostazioni e valutare una condizione.

Ad esempio, per valutare se l’utente si trova sull’host `example.com`, il modulo potrebbe presentarsi così.

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

Se si desidera rendere il nome host configurabile dall’utente per consentire l’input di un nome host e salvarlo nell’oggetto impostazioni, l’oggetto potrebbe essere simile a questo esempio.

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
1. Una [promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) che restituisce un valore booleano una volta risolta.

## Contesto del modulo Libreria

Tutti i moduli delle condizioni hanno accesso a una variabile `context` fornita quando viene chiamato il modulo. Per saperne di più [fai clic qui](./context.md).
