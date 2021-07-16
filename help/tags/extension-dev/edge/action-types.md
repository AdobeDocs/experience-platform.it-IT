---
title: Tipi di azioni per le estensioni Edge
description: Scopri come definire un modulo libreria di tipo azione per un’estensione tag in una proprietà edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 49%

---

# Tipi di azioni per le estensioni Edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo di libreria di tipo azione è progettato per eseguire un&#39;azione predefinita. L’effetto di questa azione è completamente definito dall’autore. Il modulo può essere creato come beacon o anche trasformare alcuni dati dall’evento.

>[!IMPORTANT]
>
>Questo documento descrive i tipi di azione per le estensioni edge. Se stai sviluppando un&#39;estensione web, consulta invece la guida sui [tipi di azione per le estensioni web](../web/action-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

Ad esempio, un modulo per inoltrare alcuni dati a un endpoint di terze parti potrebbe avere questo aspetto.

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

Se si desidera configurare l’endpoint dall’utente e consentire l’input e la persistenza di un endpoint nell’oggetto delle impostazioni all’interno del modulo, l’oggetto avrà un aspetto simile a questo.

```json
{
  "endpoint": "http://someendpoint.com"
}
```

Per funzionare sull’endpoint definito dall’utente, il modulo deve passare all’esempio seguente.

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

Il risultato restituito da un modulo di azione può essere qualsiasi cosa. Se l&#39;azione deve eseguire un&#39;attività asincrona, è possibile restituire una [promessa](https://developer.mozilla.org/it-IT/docs/Web/JavaScript/Reference/Global_Objects/Promise) che restituisce il risultato desiderato una volta risolta.

Il risultato dell&#39;azione viene memorizzato all&#39;interno di una chiave `ruleStash` che viene resa disponibile a tutti i moduli tramite il parametro `context` (`context.arc.ruleStash`). Ulteriori informazioni su `ruleStash` sono disponibili [qui](./context.md#rulestash).
