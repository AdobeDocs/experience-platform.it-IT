---
title: Rendering delle offerte HTML senza selettori
description: Esegui il rendering degli elementi della proposta HTML che non includono selettori fornendo metadati da applicareProposition e registrando quindi gli eventi di visualizzazione.
keywords: personalizzazione;applyPropositions;metadata;actionType;decisionScopes;visualizzare eventi;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Rendering delle offerte HTML senza selettori

Utilizza questo modello quando le proposte includono contenuto HTML, ma devi specificare dove applicarlo (selettore) e come applicarlo (tipo di azione). Per eseguire questa operazione, chiamare [`applyPropositions`](/help/collection/js/commands/applypropositions.md) con un oggetto `metadata` impostato dall&#39;ambito. I valori `actionType` supportati sono `setHtml`, `replaceHtml` e `appendHtml`.

## &#x200B;1. Gestire la visualizzazione momentanea di altri contenuti (facoltativo)

Se nascondi il contenuto durante il rendering, sei tenuto a rivelarlo al termine del rendering. Per ulteriori informazioni, vedere [Gestione visualizzazione momentanea di altri contenuti](manage-flicker.md).

## &#x200B;2. Richiedere le proposte per gli ambiti che si intende presentare

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  // Render in the next step
});
```

Per ulteriori informazioni, vedere [`personalization.decisionScopes`](/help/collection/js/commands/sendevent/personalization.md).

## &#x200B;3. Eseguire il rendering delle offerte con `applyPropositions` metadati

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: {
        selector: "#salutation",
        actionType: "setHtml"
      },
      discount: {
        selector: "#daily-special",
        actionType: "replaceHtml"
      }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return { renderedPropositions };
  });
});
```

## &#x200B;4. Registrazione degli eventi di visualizzazione per le proposte sottoposte a rendering

Gli eventi di visualizzazione non vengono inviati automaticamente quando si chiama `applyPropositions`. Al termine del rendering, utilizza una chiamata `sendEvent` che fa riferimento alle proposte sottoposte a rendering:

```js
function toDisplayPayload(propositions) {
  return propositions.map((p) => ({
    id: p.id,
    scope: p.scope,
    scopeDetails: p.scopeDetails
  }));
}

alloy("sendEvent", {
  personalization: {
    decisionScopes: ["discount", "salutation"]
  },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  }).then(({ propositions: renderedPropositions = [] }) => {
    return alloy("sendEvent", {
      xdm: {
        _experience: {
          decisioning: {
            propositions: toDisplayPayload(renderedPropositions),
            propositionEventType: { display: 1 }
          }
        }
      }
    });
  });
});
```

Per ulteriori informazioni, vedere [Gestione eventi di visualizzazione](display-events.md).

>[!TIP]
>
>Se utilizzi [eventi di pagina superiore e inferiore](top-bottom-page-events.md), questa chiamata &quot;visualizzazione record&quot; è comunemente implementata nella chiamata `sendEvent` inferiore.

## &#x200B;5. Nuova rappresentazione

Se l&#39;implementazione richiede un nuovo rendering in un secondo momento (ad esempio nelle applicazioni a pagina singola), chiamare nuovamente `applyPropositions` con le stesse proposte e gli stessi metadati:

```js
alloy("applyPropositions", {
  propositions,
  metadata: {
    discount: { selector: "#daily-special", actionType: "replaceHtml" }
  }
});
```

Se devi registrare un evento di visualizzazione per quel rendering, vedi [Gestione eventi di visualizzazione](display-events.md).
