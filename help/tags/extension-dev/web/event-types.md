---
title: Tipi di eventi per le estensioni Web
description: Scopri come definire un modulo libreria per tipi di evento per un’estensione Web in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 31%

---

# Tipi di eventi per estensioni web

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In una regola di tag , un evento è un&#39;attività che deve verificarsi per attivare una regola. Ad esempio, un&#39;estensione web potrebbe fornire un tipo di evento &quot;gesture&quot; che controlla l&#39;esecuzione di un determinato movimento del mouse o del tocco. Quando si verifica il gesto, la logica dell’evento attiva la regola.

Un modulo libreria di tipo evento è progettato per rilevare quando si verifica un&#39;attività e quindi chiamare una funzione per attivare una regola associata. L&#39;evento rilevato è personalizzabile. Ad esempio, potrebbe rilevare quando un utente compie un determinato gesto, lo scorre rapidamente o interagisce con qualcosa.

Questo documento illustra come definire i tipi di evento per un&#39;estensione Web in Adobe Experience Platform.

>[!NOTE]
>
>Questo documento presuppone che tu abbia familiarità con i moduli di libreria e con il modo in cui sono integrati nelle estensioni web. Se necessario, consulta la panoramica sul [formato dei moduli libreria](./format.md) per un&#39;introduzione alla relativa implementazione prima di proseguire con questa guida.

I tipi di evento sono definiti da estensioni e in genere consistono nei seguenti elementi:

1. Una [visualizzazione](./views.md) mostrata all&#39;interno dell&#39;interfaccia utente della raccolta dati che consente agli utenti di modificare le impostazioni per l&#39;evento.
2. Un modulo libreria emesso all’interno della libreria di runtime di tag per interpretare le impostazioni e controllare che si verifichi una determinata attività.

`module.exports` accetta sia i  `settings` che  `trigger` i parametri . Questo consente di personalizzare il tipo di evento.

```js
module.exports = function(settings, trigger) { … };
```

| Parametro | Descrizione |
| --- | --- |
| `settings` | Un oggetto contenente le impostazioni configurate dall’utente nella vista del tipo di evento. Puoi definire cosa viene inserito in questo oggetto. |
| `trigger` | Funzione chiamata dal modulo ogni volta che la regola deve essere attivata. Esiste una relazione uno-a-uno tra un oggetto `settings`, una funzione `trigger` e una regola. Ciò significa che la funzione di attivazione ricevuta per una regola non può essere utilizzata per attivare una regola diversa. |

>[!NOTE]
>
>La funzione esportata verrà chiamata una sola volta per ogni regola configurata per l’utilizzo del tipo di evento.

Utilizzando come esempio l’attività di cinque secondi trascorsi, dopo cinque secondi, l’attività si è svolta e la regola si attiverà. Il modulo avrà un aspetto simile a questo esempio.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Se si desidera che la durata sia configurabile dall&#39;utente Adobe Experience Platform, è necessaria l&#39;opzione per inserire e salvare una durata nell&#39;oggetto delle impostazioni. L’oggetto potrebbe presentarsi così:

```js
{
  "duration": 25000
}
```

Per poter funzionare sulla durata definita dall’utente, è necessario aggiornare il modulo per includerlo.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Trasmettere i dati dell’evento contestuale

Quando una regola viene attivata, spesso è utile fornire ulteriori dettagli sull&#39;evento che si è verificato. Per gli utenti che creano le regole, tali informazioni possono essere utili per ottenere un determinato comportamento. Ad esempio, se un addetto al marketing desidera creare una regola in cui viene inviato un beacon di analisi ogni volta che l’utente scorre lo schermo. L&#39;estensione deve fornire un tipo di evento `swipe` in modo che l&#39;addetto al marketing possa utilizzare questo tipo di evento per attivare la regola appropriata. Supponendo che l’addetto al marketing desideri includere l’angolo in cui si è verificato il passaggio del mouse sul beacon, sarebbe difficile farlo senza fornire ulteriori informazioni. Per fornire informazioni aggiuntive sull’evento che si è verificato, si passa un oggetto quando si chiama la funzione `trigger`. Esempio:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

L’addetto marketing può quindi utilizzare questo valore su un beacon di analisi specificando il valore `%event.swipeAngle%` in un campo di testo. Può anche accedere a `event.swipeAngle` da altri contesti (come un’azione di codice personalizzato). È possibile includere altri tipi di informazioni di evento facoltative che possono essere utili a un addetto al marketing nello stesso modo.

### [!DNL nativeEvent]

Se il tipo di evento è basato su un evento nativo (ad esempio, se l&#39;estensione fornisce un tipo di evento `click`), è consigliabile impostare la proprietà `nativeEvent` come segue.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Ciò può essere utile agli addetti marketing che vogliono poter accedere a qualsiasi informazione dell’evento nativo, ad esempio alle coordinate del cursore.

### [!DNL element]

Se esiste una relazione forte tra un elemento e l’evento che si è verificato, si consiglia di impostare la proprietà `element` sul nodo DOM dell’elemento. Ad esempio, se l’estensione fornisce un tipo di evento `click` e consente agli esperti di marketing di configurarlo in modo che la regola si attivi solo se è selezionato un elemento con ID `herobanner`. In questo caso, se l’utente seleziona il banner eroe, si consiglia di chiamare `trigger` e impostare `element` sul nodo DOM del banner eroe.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Rispetto dell’ordine delle regole

I tag consentono agli utenti di ordinare le regole. Ad esempio, un utente può creare due regole che utilizzano sia il tipo di evento orientation-change che l&#39;ordine di attivazione delle regole. Supponendo che l&#39;utente Adobe Experience Platform specifichi un valore dell&#39;ordine di `2` per l&#39;evento di modifica dell&#39;orientamento nella regola A e un valore dell&#39;ordine di `1` per l&#39;evento di modifica dell&#39;orientamento nella regola B. Questo indica che quando l’orientamento cambia su un dispositivo mobile, la regola B deve attivarsi prima della regola A (regole con valori di ordine inferiore si attivano per prime).

Come già detto, la funzione esportata nel modulo dell’evento verrà chiamata una volta per ogni regola configurata per l’utilizzo di quel tipo di evento. Ogni volta che viene chiamata la funzione esportata, viene passata una funzione `trigger` univoca associata a una regola specifica. Nello scenario appena descritto, la nostra funzione esportata verrà chiamata una volta con una funzione `trigger` associata alla regola B e poi di nuovo con una funzione `trigger` associata alla regola A. La regola B viene prima perché l&#39;utente gli ha dato un valore di ordine inferiore alla regola A. Quando il modulo libreria rileva una modifica di orientamento, è importante chiamare le funzioni `trigger` nello stesso ordine in cui sono state fornite al modulo libreria.

Nell’esempio di codice riportato di seguito, osserva che quando viene rilevata una modifica di orientamento, le funzioni di attivazione vengono chiamate nello stesso ordine in cui sono state fornite alla funzione esportata:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

In questo modo viene mantenuto l’ordine specificato dall’utente.

Se le funzioni di attivazione venissero chiamate in un ordine diverso, l’implementazione risulterebbe errata:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Le pratiche di programmazione con linguaggio naturale mantengono in genere un ordine corretto, ma è importante essere consapevoli delle implicazioni e portare avanti lo sviluppo di conseguenza.
