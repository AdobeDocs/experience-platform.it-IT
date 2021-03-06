---
title: Tipi di elementi dati per le estensioni web
description: Scopri come definire un modulo libreria di tipo elemento dati per un’estensione tag in una proprietà web.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 60%

---

# Tipi di elementi dati per estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nei tag di raccolta dati, gli elementi dati sono essenzialmente alias a parti di dati su una pagina. Questi dati si trovano nei parametri della stringa di query, nei cookie, negli elementi DOM o in altre posizioni. Le regole possono fare riferimento a un elemento dati che funge da astrazione per accedere a tali dati.

I tipi di elementi dati sono forniti da estensioni e consentono agli utenti di configurare elementi dati per accedere a parti di dati in un particolare modo. Ad esempio, un’estensione potrebbe fornire un tipo di elemento dati “elemento di archiviazione locale” in cui l’utente di può specificare il nome di un elemento specifico. Quando una regola fa riferimento all’elemento dati, l’estensione sarà in grado di cercare il valore dell’elemento nell’archiazione locale utilizzando il nome fornito dall’utente durante la configurazione dell’elemento dati.

Questo documento illustra come definire i tipi di elementi dati per un&#39;estensione Web in Adobe Experience Platform.

>[!IMPORTANT]
>
>Se stai sviluppando un&#39;estensione Edge, consulta la guida sui tipi di elementi dati [per le estensioni edge](../edge/data-element-types.md) .
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli di libreria e con la loro integrazione nelle estensioni web. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di elementi dati sono in genere costituiti dai seguenti elementi:

1. Una [visualizzazione](./views.md) mostrata nell&#39;interfaccia utente di Raccolta dati che consente agli utenti di modificare le impostazioni per l&#39;elemento dati.
2. Un modulo libreria emesso all&#39;interno della libreria di runtime di tag per interpretare le impostazioni e recuperare parti di dati.

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
