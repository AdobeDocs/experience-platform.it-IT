---
title: Tipi di azioni per le estensioni Edge
description: Scopri come definire un modulo libreria di tipo azione per un’estensione tag in una proprietà edge.
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 66%

---

# Tipi di azioni per le estensioni Edge

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In una regola di tag, un&#39;azione viene eseguita dopo che le condizioni della regola hanno superato la valutazione. I tipi di azione vengono forniti dalle estensioni e i loro effetti sono interamente definiti dall&#39;autore dell&#39;estensione.

Ad esempio, un’estensione potrebbe fornire un tipo di azione “show support chat” che potrebbe mostrare una finestra di dialogo con la chat di supporto per aiutare gli utenti che riscontrano difficoltà nel concludere un acquisto.

Questo documento illustra come definire i tipi di azioni per un&#39;estensione Edge in Adobe Experience Platform.

>[!IMPORTANT]
>
>Se stai sviluppando un&#39;estensione web, consulta invece la guida sui [tipi di azione per le estensioni web](../web/action-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli di libreria e con il modo in cui sono integrati nelle estensioni edge. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di azione in genere consistono nei seguenti elementi:

1. Visualizzazione nell’interfaccia utente Experience Platform e nell’interfaccia utente di raccolta dati che consente agli utenti di modificare le impostazioni dell’azione.
2. Un modulo libreria emesso all&#39;interno della libreria di runtime di tag per interpretare le impostazioni ed eseguire un&#39;azione.

Ad esempio, un modulo l’inoltro di alcuni dati a un endpoint di terze parti potrebbe presentarsi come segue:

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

Se si desidera rendere l’endpoint configurabile dall’utente e consentire l’input e la persistenza di un endpoint nell’oggetto impostazioni all’interno del modulo, l’oggetto avrà un aspetto simile al seguente:

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Per utilizzare il nome dell’endpoint definito dall’utente, è necessario modificare il modulo come segue:

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## Risultato azione

Il risultato restituito da un modulo di azione può essere qualsiasi cosa. Se l&#39;azione deve eseguire un&#39;attività asincrona, è possibile restituire una [promessa](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) che restituisce il risultato desiderato una volta risolta.

Il risultato dell&#39;azione viene memorizzato all&#39;interno di una chiave `ruleStash` che viene resa disponibile a tutti i moduli tramite il parametro `context` (`context.arc.ruleStash`). Ulteriori informazioni su `ruleStash` sono disponibili [qui](./context.md#rulestash).
