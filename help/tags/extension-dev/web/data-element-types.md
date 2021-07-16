---
title: Tipi di elementi dati per le estensioni web
description: Scopri come definire un modulo libreria di tipo elemento dati per un’estensione tag in una proprietà web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 70%

---

# Tipi di elementi dati per le estensioni Edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Lo scopo di un modulo di raccolta di tipi di elementi dati è quello di recuperare una parte di dati. Il metodo per questo recupero è personalizzabile. I diversi tipi di elementi dati consentono agli utenti Adobe Experience Platform di recuperare dati dall’archiviazione locale, da un cookie o da un elemento DOM.

>[!IMPORTANT]
>
>Questo documento fornisce informazioni sui tipi di elementi dati per le estensioni Web. Se stai sviluppando un’estensione Edge, consulta invece la guida sui [tipi di elementi dati per le estensioni Edge](../edge/data-element-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

Considera una situazione in cui desideri consentire agli utenti di recuperare dei dati da un elemento nell’archiviazione locale denominato `productName`. Il modulo potrebbe presentarsi così:

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

Se si desidera rendere configurabile il nome dell&#39;elemento di archiviazione locale dall&#39;utente Adobe Experience Platform, è possibile consentire all&#39;utente di immettere un nome e quindi salvare il nome nell&#39;oggetto `settings`. L’oggetto potrebbe presentarsi così:

```js
{
  itemName: "campaignId"
}
```

Per poter utilizzare il nome dell’elemento di archiviazione locale definito dall’utente, è necessario modificare il modulo in:

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## Supporto di valori predefiniti

Gli utenti possono configurare un valore predefinito per qualsiasi elemento dati. Se il modulo libreria dell’elemento dati restituisce il valore `undefined` o `null`, verrà automaticamente sostituito dal valore predefinito configurato dall’utente per l’elemento dati.

## Dati contestuali sugli eventi

Se l’elemento dati viene recuperato a seguito dell’attivazione di una regola (ad esempio, se gli elementi dati vengono utilizzati nelle condizioni e nele azioni della regola), al modulo verrà trasmesso un secondo argomento contenente informazioni contestuali relative all’evento che ha attivato la regola. Può risultare utile in alcuni casi e vi si può accedere nel modo seguente:

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
