---
title: Tipi di azioni per le estensioni web
description: Scopri come definire un modulo libreria di tipo azione per un’estensione tag in una proprietà web.
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 70%

---

# Tipi di azioni per le estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nel contesto dei tag di raccolta dati, un&#39;azione è qualcosa che viene eseguita dopo un evento di regola e tutte le condizioni hanno superato la valutazione.

Ad esempio, un’estensione potrebbe fornire un tipo di azione “show support chat” che potrebbe mostrare una finestra di dialogo con la chat di supporto per aiutare gli utenti che riscontrano difficoltà nel concludere un acquisto.

Questo documento illustra come definire i tipi di azioni per un&#39;estensione Web in Adobe Experience Platform.

>[!IMPORTANT]
>
>Questo documento descrive i tipi di azione per le estensioni web. Se stai sviluppando un’estensione Edge, consulta invece la guida sui [tipi di azione per le estensioni Edge](../edge/action-types.md).
>
>Questo documento presuppone anche che tu abbia familiarità con i moduli di libreria e con la loro integrazione nelle estensioni web. Per un&#39;introduzione, vedere la panoramica sulla [formattazione del modulo libreria](./format.md) prima di tornare a questa guida.

I tipi di azione in genere consistono nei seguenti elementi:

1. A [visualizzare](./views.md) nell’interfaccia utente di Experience Platform e nell’interfaccia utente di raccolta dati, che consente agli utenti di modificare le impostazioni dell’azione.
2. Un modulo libreria emesso all&#39;interno della libreria di runtime di tag per interpretare le impostazioni ed eseguire un&#39;azione.

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

Ad esempio, affinché il messaggio possa essere configurato dall’utente di Adobe Experience Platform, puoi consentire all’utente di inserire e salvare un messaggio nell’oggetto impostazioni. L’oggetto si presente simile a questo:

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

Un secondo argomento deve quindi essere passato al modulo contenente le informazioni contestuali sull’evento che attiva la regola. Può risultare utile in alcuni casi e vi si può accedere nel modo seguente:

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
