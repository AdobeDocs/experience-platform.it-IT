---
title: Tipi di elementi dati per le estensioni Edge
description: Scopri come definire un modulo di libreria di tipo elemento dati per un’estensione tag in una proprietà edge.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 59%

---

# Tipi di elementi dati nelle estensioni edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un modulo di libreria di tipo-elemento-dati recupera una parte di dati. L’autore del modulo determina il modo in cui viene recuperato questo elemento di dati. Ad esempio, è possibile utilizzare un tipo di elemento dati per consentire agli utenti Adobe Experience Platform di recuperare una parte di dati dal livello XDM o dal relativo livello dati personalizzato.

>[!IMPORTANT]
>
>Questo documento descrive i tipi di elementi dati per le estensioni edge. Se stai sviluppando un&#39;estensione web, consulta invece la guida sui [tipi di elementi dati per le estensioni web](../web/data-element-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli libreria e con la loro integrazione nelle estensioni tag. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

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
