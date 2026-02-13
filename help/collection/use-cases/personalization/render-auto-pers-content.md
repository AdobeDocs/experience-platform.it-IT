---
title: Esegui automaticamente il rendering delle proposte di azione DOM
description: Utilizza Web SDK per eseguire automaticamente il rendering delle proposte di azione DOM idonee e gestire scenari di rendering comuni per applicazioni a pagina singola.
keywords: personalizzazione;renderDecisions;dom-action;sendEvent;applyPropositions;applicazione a pagina singola;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Rendering automatico delle proposte di azioni DOM

Utilizza questo modello quando la risposta di personalizzazione include elementi di proposta con lo schema:

**`https://ns.adobe.com/personalization/dom-action`**

Questi elementi includono in genere un selettore e un tipo di azione (ad esempio, `setHtml`) che il Web SDK può applicare automaticamente quando `renderDecisions` è abilitato.

## &#x200B;1. Gestire la visualizzazione momentanea di altri contenuti (facoltativo)

Per evitare sfarfallii durante l’applicazione di contenuti personalizzati, utilizza l’approccio di gestione consigliato per la visualizzazione momentanea di altri contenuti per l’implementazione. Consulta [Gestire la visualizzazione momentanea di altri contenuti](manage-flicker.md) per informazioni sulle opzioni disponibili.

## &#x200B;2. Richiedere e rendere note le decisioni per il rendering automatico

Impostare `renderDecisions` su `true` quando si chiama il comando `sendEvent`. Se omessa, la proprietà `renderDecisions` viene impostata automaticamente su false.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

Facoltativamente, se devi richiedere posizionamenti specifici, includi `personalization.decisionScopes`:

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    decisionScopes: ["hero-banner", "recommendations"]
  },
  xdm: { }
});
```

Per ulteriori informazioni, vedere l&#39;oggetto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) nel comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;3. Eventi di visualizzazione

Se si imposta `renderDecisions` su `true` e si imposta `personalization.sendDisplayEvent` su `true` o lo si omette, Web SDK invia gli eventi di visualizzazione subito dopo il rendering della personalizzazione.

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: {
    // sendDisplayEvent defaults to true when omitted
  },
  xdm: { }
});
```

Consulta [Gestisci eventi di visualizzazione](display-events.md) per le opzioni alternative che soddisfano le esigenze dell&#39;implementazione, ad esempio quando utilizzi [eventi di pagina superiore e inferiore](top-bottom-page-events.md).

## &#x200B;4. Modifiche alla vista dell’applicazione a pagina singola e nuovo rendering

Per le applicazioni a pagina singola, includere `viewName` sugli eventi di modifica della visualizzazione.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```

Se l’applicazione a pagina singola esegue nuovamente il rendering dell’interfaccia utente per la stessa visualizzazione senza un nuovo recupero delle decisioni, puoi riapplicare le proposte restituite in precedenza:

```js
let lastPropositions = [];

alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    web: { webPageDetails: { viewName: "cart" } }
  }
}).then(({ propositions = [] }) => {
  lastPropositions = propositions;
});

// Later, after a UI re-render:
alloy("applyPropositions", {
  propositions: lastPropositions
});
```

Per ulteriori informazioni, vedere [`applyPropositions`](/help/collection/js/commands/applypropositions.md).

>[!NOTE]
>
>Il comando `applyPropositions` non invia automaticamente eventi di visualizzazione. Se devi registrare &quot;display&quot; per gli scenari di rendering, consulta [Gestisci eventi di visualizzazione](display-events.md).
