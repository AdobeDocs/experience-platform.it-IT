---
title: Rendering manuale delle proposte
description: Esegui il rendering del contenuto della proposta utilizzando la tua logica di interfaccia utente (HTML, JSON o schemi personalizzati), quindi registra gli eventi di visualizzazione.
keywords: personalizzazione;proposte;rendering manuale;sendEvent;decisionScopes;visualizzare eventi;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Rendering manuale delle proposte

Utilizza questo pattern quando hai bisogno di un controllo completo sul modo in cui vengono applicati gli elementi della proposta. Ad esempio, stai componendo un’interfaccia utente complessa da contenuti JSON oppure desideri applicare regole aziendali personalizzate prima del rendering.

## &#x200B;1. Richiedere proposte

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["salutation", "discount"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Per ulteriori informazioni, vedere l&#39;oggetto [`personalization`](/help/collection/js/commands/sendevent/personalization.md) nel comando [`sendEvent`](/help/collection/js/commands/sendevent/overview.md).

## &#x200B;2. Rendering degli elementi della proposta (esempio)

Quando si esegue il rendering manuale delle proposte, queste possono assumere molte forme diverse. Di seguito è riportato un esempio minimo che trova una proposta in base all’ambito, quindi applica il primo elemento di contenuto HTML trovato.

```js
function findPropositionByScope(propositions, scope) {
  return propositions.find((p) => p.scope === scope);
}

function renderHtmlInto(selector, html) {
  const el = document.querySelector(selector);
  if (!el) return;
  el.innerHTML = html;
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const discount = findPropositionByScope(propositions, "discount");
  if (!discount) return { propositions, rendered: [] };

  const htmlItem = discount.items?.find(
    (i) => i.schema === "https://ns.adobe.com/personalization/html-content-item"
  );

  if (!htmlItem) return { propositions, rendered: [] };

  renderHtmlInto("#daily-special", htmlItem.data.content);
  return { propositions, rendered: [discount] };
});
```

>[!IMPORTANT]
>
>Se esegui il rendering di HTML, accertati che sia sicuro per il tuo ambiente. Considera il rendering dei contenuti come limite di sicurezza (bonifica, fonti attendibili e considerazioni sui CSP).

## &#x200B;3. Registrare gli eventi di visualizzazione per il rendering

Per le proposte sottoposte a rendering manuale, gli eventi di visualizzazione vengono registrati tramite `sendEvent` chiamate che fanno riferimento alle proposte sottoposte a rendering.

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

// Example: record display for the propositions you actually rendered.
alloy("sendEvent", {
  xdm: {
    _experience: {
      decisioning: {
        propositions: toDisplayPayload(renderedPropositions),
        propositionEventType: { display: 1 }
      }
    }
  }
});
```

Per ulteriori informazioni, vedere [Gestione eventi di visualizzazione](display-events.md).

## &#x200B;4. Nuova rappresentazione

Quando le modifiche dell’interfaccia utente richiedono un nuovo rendering, esegui nuovamente la logica di rendering manuale in base ai dati della proposta memorizzati in cache (o recuperali di nuovo, se necessario). Se devi registrare una visualizzazione per gli scenari di rendering, consulta [Gestione eventi di visualizzazione](display-events.md).
