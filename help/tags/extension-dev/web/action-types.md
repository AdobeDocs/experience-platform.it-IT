---
title: Tipi di azioni per le estensioni web
description: Scopri come definire un modulo libreria di tipo azione per un’estensione tag in una proprietà web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 65%

---

# Tipi di azioni per le estensioni web

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo libreria di tipi di azione è destinato a eseguire un&#39;azione predefinita. Ciò che questa azione fa dipende interamente da te. Desideri inviare un beacon, mostrare un’offerta, ringraziare l’utente per la visita, salvare un cookie o aprire una chat di supporto?

>[!IMPORTANT]
>
>Questo documento descrive i tipi di azione per le estensioni web. Se stai sviluppando un’estensione Edge, consulta invece la guida sui [tipi di azione per le estensioni Edge](../edge/action-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Ad esempio, per rendere il messaggio configurabile dall’utente Adobe Experience Platform, puoi consentire all’utente di inserire e salvare un messaggio nell’oggetto settings. L&#39;oggetto ha un aspetto simile a questo:

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

Per poter utilizzare il messaggio definito dall’utente, il modulo deve essere modificato come segue:

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## Dati contestuali sugli eventi

Un secondo argomento deve quindi essere passato al modulo che contiene le informazioni contestuali sull&#39;evento che attiva la regola. Può risultare utile in alcuni casi e vi si può accedere nel modo seguente:

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
