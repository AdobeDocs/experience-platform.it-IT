---
title: Gestire gli eventi di visualizzazione nel Web SDK
description: Spiega cosa sono gli eventi di visualizzazione e come utilizzarli nel Web SDK.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
keywords: personalizzazione;visualizzare eventi;sendEvent;renderDecisions;applyPropositions;propositions;
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Gestire gli eventi di visualizzazione nel Web SDK

Gli eventi di visualizzazione informano i servizi di personalizzazione o analisi che è stato visualizzato un contenuto personalizzato specifico per l’utente. L&#39;invio di eventi di visualizzazione migliora la precisione della generazione di rapporti aiutando i sistemi a valle a distinguere tra contenuto *richiesto* e contenuto *effettivamente visualizzato*.

## Invia automaticamente eventi di visualizzazione

Gli eventi di visualizzazione automatica sono in genere l’opzione più semplice. Vengono inviati immediatamente dopo il completamento del rendering dei contenuti idonei da parte di Web SDK dalla risposta `sendEvent`, in modo da migliorare l&#39;accuratezza del reporting.

Per inviare automaticamente gli eventi di visualizzazione, utilizzare una chiamata `sendEvent` che imposta `renderDecisions` su `true` e imposta `personalization.sendDisplayEvent` su `true` (oppure omettere, poiché `true` è l&#39;impostazione predefinita):

```js
alloy("sendEvent", {
  renderDecisions: true,
  personalization: { }, // sendDisplayEvent defaults to true
  xdm: {
    web: {
      webPageDetails: {
        name: "home"
      }
    }
  }
});
```

>[!NOTE]
>
>Gli eventi di visualizzazione automatica dipendono dal rendering gestito da SDK. Se esegui manualmente il rendering del contenuto (anche utilizzando `applyPropositions`), devi inviare gli eventi di visualizzazione esplicitamente utilizzando `sendEvent`.

## Invia eventi di visualizzazione nelle chiamate `sendEvent` successive

L&#39;inclusione di eventi di visualizzazione in una chiamata `sendEvent` successiva è utile quando si desidera allegare dati di caricamento pagina aggiuntivi che non sono disponibili quando si richiede la personalizzazione. Viene comunemente utilizzato quando si implementano [eventi di pagina superiore e inferiore](/help/collection/use-cases/personalization/top-bottom-page-events.md). Implementare correttamente gli eventi di visualizzazione in questo modo consente di evitare problemi con [Percentuale non recapitate](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/bounce-rate) in Adobe Analytics.

1. Nella chiamata `sendEvent` iniziale (spesso nella parte superiore della pagina), richiedere ed eseguire il rendering del contenuto, ma eliminare gli eventi di visualizzazione automatica impostando `renderDecisions` su `true` e `personalization.sendDisplayEvent` su `false`:

   ```js
   alloy("sendEvent", {
     renderDecisions: true,
     personalization: { sendDisplayEvent: false },
     xdm: {
       web: {
         webPageDetails: {
            name: "home"
         }
       }
     }
   });
   ```

1. In seguito (spesso nella parte inferiore della pagina), chiama `sendEvent` con un payload XDM che include eventi di visualizzazione per le proposte di cui è stato eseguito il rendering dopo la richiesta precedente impostando [`personalization.includeRenderedPropositions`](/help/collection/js/commands/sendevent/personalization.md) su `true`:

   ```js
   alloy("sendEvent", {
     personalization: { includeRenderedPropositions: true },
     xdm: {
       // Add any additional page load telemetry you want to send here
       web: {
         webPageDetails: {
           name: "home"
         }
       }
     }
   });
   ```

>[!NOTE]
>
>Quando si utilizza `includeRenderedPropositions`, vengono incluse solo le proposte di cui è stato eseguito il rendering automatico e la cui visualizzazione è stata eliminata.

## Inviare eventi di visualizzazione per le proposte sottoposte a rendering manuale

Se esegui il rendering del contenuto manualmente (rendering completamente manuale o utilizzo di `applyPropositions`), devi inviare gli eventi di visualizzazione in modo esplicito utilizzando il comando `sendEvent`. Chiama `sendEvent` con un payload XDM che include le seguenti proprietà:

* `_experience.decisioning.propositions` contenente le proposte sottoposte a rendering&#39; `id`, `scope` e `scopeDetails`
* `_experience.decisioning.propositionEventType.display` impostato su `1`

I due esempi seguenti utilizzano questa funzione helper per generare il payload XDM dell’evento di visualizzazione:

```js
function buildDisplayEventXdm(renderedPropositions) {
  return {
    eventType: "decisioning.propositionDisplay",
    _experience: {
      decisioning: {
        propositions: renderedPropositions.map(({ id, scope, scopeDetails }) => ({
          id,
          scope,
          scopeDetails
        })),
        propositionEventType: { display: 1 }
      }
    }
  };
}
```

Nell&#39;esempio seguente viene utilizzato il rendering manuale con gli eventi di visualizzazione:

```js
function renderExample(propositions) {
  // Your custom logic here. Return ONLY the propositions that were actually rendered.
  // For example: return [propositions[0]];
  return [];
}

alloy("sendEvent", {
  personalization: { decisionScopes: ["discount"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  const renderedPropositions = renderExample(propositions);
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

Nell&#39;esempio seguente viene utilizzato il comando `applyPropositions` con eventi di visualizzazione. Catena `sendEvent`, `applyPropositions`, quindi un altro `sendEvent` insieme:

```js
alloy("sendEvent", {
  personalization: { decisionScopes: ["discount", "salutation"] },
  xdm: { }
}).then(({ propositions = [] }) => {
  return alloy("applyPropositions", {
    propositions,
    metadata: {
      salutation: { selector: "#salutation", actionType: "setHtml" },
      discount: { selector: "#daily-special", actionType: "replaceHtml" }
    }
  });
}).then(({ propositions: renderedPropositions = [] }) => {
  if (!renderedPropositions.length) { return; }
  return alloy("sendEvent", { xdm: buildDisplayEventXdm(renderedPropositions) });
});
```

## Errori comuni da evitare

* **Invia eventi di visualizzazione prima del completamento del rendering**: invia eventi di visualizzazione dopo il completamento del rendering automatico, dopo la risoluzione di `applyPropositions` o dopo il completamento della logica di rendering manuale.
* **Invia eventi di visualizzazione per le proposte di cui non è stato eseguito il rendering**: includi solo le proposte effettivamente visualizzate dall&#39;utente.
* **Eliminazione di`scopeDetails`**: inclusione di `scopeDetails` dall&#39;oggetto proposition durante l&#39;invio di eventi di visualizzazione.
