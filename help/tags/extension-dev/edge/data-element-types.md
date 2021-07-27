---
title: Tipi di elementi dati per le estensioni Edge
description: Scopri come definire un modulo di libreria di tipo elemento dati per un’estensione tag in una proprietà edge.
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 35%

---

# Tipi di elementi dati nelle estensioni edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nei tag, gli elementi dati sono alias per parti di dati su una pagina web o mobile, indipendentemente da dove si trovano all’interno dell’evento ricevuto dal server. Le regole possono fare riferimento a un elemento dati che funge da astrazione per accedere a tali dati. Quando la posizione dei dati cambia in futuro (ad esempio se si modifica la chiave evento che contiene il valore), è possibile riconfigurare un singolo elemento dati mentre tutte le regole che vi fanno riferimento possono rimanere invariate.

I tipi di elementi dati vengono forniti dalle estensioni e l’autore dell’estensione determina il modo in cui viene recuperato questo elemento dati. Ad esempio, è possibile utilizzare un tipo di elemento dati per consentire agli utenti Adobe Experience Platform di recuperare una parte di dati dal livello XDM o dal relativo livello dati personalizzato.

Questo documento illustra come definire i tipi di elementi dati per un’estensione edge in Adobe Experience Platform.

>[!IMPORTANT]
>
>Se stai sviluppando un&#39;estensione web, consulta invece la guida sui tipi di elementi dati [per estensioni web](../web/data-element-types.md) .
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli di libreria e con il modo in cui sono integrati nelle estensioni edge. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di elementi dati sono in genere costituiti dai seguenti elementi:

1. Visualizzazione nell’interfaccia utente di raccolta dati che consente agli utenti di modificare le impostazioni per l’elemento dati.
2. Un modulo libreria emesso all&#39;interno della libreria di runtime di tag per interpretare le impostazioni e recuperare parti di dati.

Se desideri consentire agli utenti di recuperare una parte di dati dal livello dati personalizzato, il modulo potrebbe avere un aspetto simile a questo esempio.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Se si desidera che i dati restituiti per il livello dati siano configurabili dall&#39;utente Adobe Experience Platform, è possibile consentire all&#39;utente di immettere un nome chiave e quindi salvare il nome nell&#39;oggetto `settings`. L’oggetto potrebbe presentarsi così.

```js
{
  keyName: "campaignId"
}
```

Per poter utilizzare il nome dell’elemento di archiviazione locale definito dall’utente, è necessario modificare il modulo in:

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## Contesto del modulo Libreria

Tutti i moduli di elementi dati hanno accesso a una variabile `context` fornita quando viene chiamato il modulo. Per saperne di più [fai clic qui](./context.md).
