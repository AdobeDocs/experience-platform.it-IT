---
title: Tipi di condizioni per le estensioni web
description: Scopri come definire un modulo libreria di tipo condizione per un’estensione tag in una proprietà web.
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 69%

---

# Tipi di condizioni per le estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nel contesto di una regola, una condizione viene valutata dopo che si è verificato un evento. Tutte le condizioni devono restituire true affinché la regola possa continuare l’elaborazione. L’eccezione si verifica quando gli utenti inseriscono esplicitamente le condizioni in un bucket di &quot;eccezione&quot;, nel qual caso tutte le condizioni all’interno del bucket devono restituire false per consentire alla regola di continuare l’elaborazione.

Ad esempio, un’estensione potrebbe fornire un tipo di condizione “viewport contains” in cui l’utente di potrebbe specificare un selettore CSS. Quando la condizione viene valutata sul sito web del client, l’estensione sarà in grado di trovare elementi che corrispondono al selettore CSS e restituire se uno di essi è contenuto nella finestra dell’utente.

Questo documento illustra come definire i tipi di condizioni per un’estensione web in Adobe Experience Platform.

>[!NOTE]
>
>Se stai sviluppando un’estensione Edge, consulta invece la guida sui [tipi di condizioni per le estensioni Edge](../edge/condition-types.md).
>
>In questo documento si presuppone che tu abbia familiarità con i moduli libreria e sul modo in cui vengono integrati nelle estensioni web. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di condizione sono in genere i seguenti:

1. [view](./views.md) nell&#39;interfaccia utente di Experience Platform e nell&#39;interfaccia utente di Data Collection che consente agli utenti di modificare le impostazioni per la condizione.
2. Modulo libreria emesso all’interno della libreria runtime dei tag per interpretare le impostazioni e valutare una condizione.

Un modulo libreria di tipo condizione ha un obiettivo: valutare se qualcosa è vero o falso. Sta a te definire ciò che verrà valutato.

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
