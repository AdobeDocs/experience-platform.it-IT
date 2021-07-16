---
title: Tipi di condizioni per le estensioni web
description: Scopri come definire un modulo libreria di tipo condizione per un’estensione tag in una proprietà web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 86%

---

# Tipi di condizioni per le estensioni web

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta il seguente[documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo libreria per tipi di condizione ha un obiettivo: valutare se qualcosa è vero o falso. Sta a te definire ciò che verrà valutato.

>[!NOTE]
>
>Questo documento descrive i tipi di condizioni per le estensioni web. Se stai sviluppando un’estensione Edge, consulta invece la guida sui [tipi di condizioni per le estensioni Edge](../edge/condition-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

Ad esempio, per valutare se l’utente si trova sull’host `example.com`, il modulo potrebbe presentarsi così:

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

Considera ora la situazione in cui desideri che l’utente di Adobe Experience Platform possa configurare il nome dell’host. Puoi consentire all’utente di inserire un nome di host e quindi di salvarlo nell’oggetto impostazioni. L’oggetto potrebbe presentarsi così:

```js
{
  "hostname": "example.com"
}
```

Per utilizzare il nome dell’host definito dall’utente, è necessario modificare il modulo come segue:

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## Dati contestuali sugli eventi

Al modulo viene trasmesso un secondo argomento che contiene informazioni contestuali relative all’evento che ha attivato la regola. Può risultare utile in alcuni casi e vi si può accedere nel modo seguente:

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

L’oggetto `event` deve contenere le seguenti proprietà:

| Proprietà | Descrizione |
| --- | --- |
| `$type` | Stringa che descrive il nome dell’estensione e il nome dell’evento, separati da un punto. Ad esempio, `youtube.play`. |
| `$rule` | Oggetto contenente informazioni sulla regola attualmente in esecuzione. L’oggetto deve contenere le seguenti sotto-proprietà:<ul><li>`id`: ID della regola attualmente in esecuzione.</li><li>`name`: nome della regola attualmente in esecuzione.</li></ul> |

L’estensione che fornisce il tipo di evento che ha attivato la regola può facoltativamente aggiungere altre informazioni utili a questo oggetto `event`.
