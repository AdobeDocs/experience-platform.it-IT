---
title: track()
description: Attiva una regola di chiamata diretta.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

Il metodo `_satellite.track()` consente di attivare una [regola di chiamata diretta](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>Adobe considera `_satellite.track()` un **metodo di implementazione legacy**. Anche se è ancora completamente supportato, Adobe consiglia vivamente di utilizzare pratiche di implementazione più moderne, come [Adobe Client Data Layer](/help/tags/extensions/client/client-data-layer/overview.md), che è l&#39;approccio consigliato per le nuove implementazioni.
>
>Se scegli di utilizzare `_satellite.track()` sul tuo sito, **proteggi ogni chiamata** in modo che il tuo sito non sia strettamente collegato alla libreria di tag. Se non è protetto, la rimozione della proprietà tag causerà errori in tutti i riferimenti all&#39;oggetto `_satellite`.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Quando si chiama `_satellite.track()` utilizzando l&#39;identificatore configurato nell&#39;interfaccia utente dei tag, la regola viene attivata immediatamente. La chiamata di questo metodo funge solo da evento regola; le condizioni della regola vengono comunque applicate prima dell&#39;esecuzione delle azioni della regola. Più regole di chiamata diretta possono utilizzare lo stesso identificatore, consentendo di attivare tutte queste regole contemporaneamente utilizzando una singola chiamata `_satellite.track()`. Ogni regola attivata controlla ancora le proprie condizioni prima di intraprendere azioni, anche se più regole condividono lo stesso identificatore.

## Campi disponibili

Il metodo `_satellite.track()` supporta due argomenti:

| Nome | Tipo | Obbligatorio | Descrizione |
|---|---|---|---|
| **`identifier`** | `string` | Sì | L’identificatore della regola di chiamata diretta. Puoi impostare questo identificatore durante la configurazione della regola nell’interfaccia utente dei tag. |
| **`detail`** | `unknown` | No | Un payload opzionale contenente tutte le informazioni desiderate. Durante la configurazione di una regola, puoi accedere al payload utilizzando `event.detail` (codice personalizzato) o `%event.detail%` (campi di testo che supportano la notazione dell&#39;elemento dati). |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
