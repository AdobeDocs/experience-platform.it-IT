---
title: Tipi di elementi dati per le estensioni Edge
description: Scopri come definire un modulo libreria data-element-type per un’estensione tag in una proprietà edge.
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 51%

---

# Tipi di elementi dati nelle estensioni Edge

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nei tag, gli elementi dati sono alias per parti di dati su una pagina web o mobile, indipendentemente da dove si trovano i dati all’interno dell’evento ricevuto dal server. Le regole possono fare riferimento a un elemento dati che funge da astrazione per accedere a tali dati. Quando la posizione dei dati cambia in futuro (ad esempio, quando si modifica la chiave dell’evento che contiene il valore), è possibile riconfigurare un singolo elemento dati mantenendo invariate tutte le regole che vi fanno riferimento.

I tipi di elementi dati vengono forniti dalle estensioni e l’autore dell’estensione determina il modo in cui vengono recuperati questi dati. Ad esempio, è possibile utilizzare un tipo di elemento dati per consentire agli utenti Adobe Experience Platform di recuperare una parte di dati dal livello XDM o dal relativo livello dati personalizzato.

Questo documento illustra come definire i tipi di elementi dati per un’estensione Edge in Adobe Experience Platform.

>[!IMPORTANT]
>
>Se stai sviluppando un&#39;estensione Web, consulta invece la guida sui [tipi di elementi dati per le estensioni Web](../web/data-element-types.md).
>
>In questo documento si presuppone che tu abbia familiarità con i moduli libreria e sul modo in cui vengono integrati nelle estensioni Edge. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di elementi dati sono in genere costituiti dai seguenti elementi:

1. Una vista mostrata nell’interfaccia di Experience Platform e nell’interfaccia di Data Collection che consente agli utenti di modificare le impostazioni per l’elemento dati.
2. Modulo libreria emesso all’interno della libreria runtime di tag per interpretare le impostazioni e recuperare i dati.

Se desideri consentire agli utenti di recuperare una parte di dati dal livello dati personalizzato, il modulo potrebbe avere un aspetto simile a questo esempio.

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

Se desideri che il nome dell’elemento nell’archiviazione locale possa essere configurato dall’utente di Adobe Experience Platform, puoi consentire agli utenti di immettere un nome chiave e quindi di salvarlo nell’oggetto `settings`. L’oggetto potrebbe presentarsi così.

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
