---
title: Configurare gli eventi di inizio e fine pagina in Web SDK
description: Questo articolo spiega come utilizzare la parte superiore e inferiore degli eventi di pagina in Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 1%

---


# Configurare gli eventi di inizio e fine pagina in Web SDK

Quando desideri offrire esperienze personalizzate ai clienti, il tempo di caricamento di una pagina web è essenziale.

Per ottimizzare i tempi di caricamento e distribuire la personalizzazione il più rapidamente possibile, Web SDK supporta la configurazione degli eventi di inizio e fine pagina.

La parte superiore e inferiore degli eventi di pagina descrivono un metodo per caricare in modo asincrono vari elementi nella pagina, mantenendo al minimo il tempo di caricamento della pagina.

Questa configurazione riduce al minimo il tempo di attesa per il caricamento del contenuto personalizzato da parte di un utente.

In termini di precisione delle metriche, Adobe Analytics può ignorare gli eventi nella parte superiore della pagina, il che consente una registrazione più accurata delle metriche, in quanto viene registrato un solo hit pagina (la parte inferiore dell’evento pagina).

## Casi d’uso {#use-cases}

Un rivenditore di abbigliamento sportivo desidera offrire esperienze personalizzate ai propri acquirenti, riducendo al minimo l’attrito degli utenti quando visitano il sito web, il tutto pur essendo in grado di raccogliere in modo accurato le metriche dei visitatori.

Utilizzando gli eventi di inizio e fine pagina in Web SDK, il team marketing può configurare la distribuzione della personalizzazione nel modo più ottimale:

* Web SDK invia una richiesta di personalizzazione che viene caricata non appena la pagina inizia a caricarsi. Questo è un evento di inizio pagina.
* Al termine del caricamento della pagina, viene registrato un evento di visualizzazione della pagina. Questo accade più avanti nel processo di caricamento della pagina. Questo è un evento nella parte inferiore della pagina.

## Esempio di evento all’inizio della pagina {#top-of-page}

L’esempio di codice seguente esemplifica una parte superiore della configurazione dell’evento della pagina che richiede la personalizzazione ma non [inviare eventi di visualizzazione](../personalization/display-events.md#send-sendEvent-calls) per le proposte sottoposte a rendering automatico. Il [eventi di visualizzazione](../personalization/display-events.md#send-sendEvent-calls) verrà inviato come parte dell’evento di fine pagina.

>[!BEGINTABS]

>[!TAB Evento all’inizio della pagina]

```js
alloy("sendEvent", {
  type: "decisioning.propositionFetch",
  renderDecisions: true,
  personalization: {
    sendDisplayEvent: false
  }
});
```

| Parametro | Obbligatorio/facoltativo | Descrizione |
|---|---|---|
| `type` | Obbligatorio | Imposta questo parametro su `decisioning.propositionFetch`. Questo tipo di evento speciale comunica ad Adobe Analytics di eliminare questo evento. Quando utilizzi il Customer Journey Analytics, puoi anche impostare un filtro per eliminare questi eventi. |
| `renderDecisions` | Obbligatorio | Imposta questo parametro su `true`. Questo parametro indica a Web SDK di eseguire il rendering delle decisioni restituite dalla rete Edge. |
| `personalization.sendDisplayEvent` | Obbligatorio | Imposta questo parametro su `false`. In questo modo si interrompe l’invio degli eventi di visualizzazione. |

>[!ENDTABS]

## Esempi di eventi nella parte inferiore della pagina {#bottom-of-page}

>[!BEGINTABS]

>[!TAB Proposizioni con rendering automatico]

L’esempio di codice seguente esemplifica una parte inferiore della configurazione dell’evento di pagina che invia eventi di visualizzazione per proposte di cui è stato eseguito automaticamente il rendering sulla pagina, ma per le quali gli eventi di visualizzazione sono stati soppressi in [inizio pagina](#top-of-page) evento.

>[!NOTE]
>
>In questo scenario, devi chiamare l’evento in fondo alla pagina _dopo_ nella parte superiore della pagina uno. Tuttavia, per l’evento nella parte inferiore della pagina non è necessario attendere il completamento della parte superiore della pagina 1.

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parametro | Obbligatorio/facoltativo | Descrizione |
|---|---|---|
| `personalization.includeRenderedPropositions` | Obbligatorio | Imposta questo parametro su `true`. Questo consente l’invio di eventi di visualizzazione che sono stati soppressi nella parte superiore dell’evento della pagina. |
| `xdm` | Facoltativo | Utilizza questa sezione per includere tutti i dati necessari per l’evento nella parte inferiore della pagina. |

>[!TAB Proposizioni sottoposte a rendering manuale]

L’esempio di codice seguente esemplifica una parte inferiore della configurazione dell’evento di pagina che invia eventi di visualizzazione per proposte di cui è stato eseguito il rendering manuale sulla pagina (ad esempio per ambiti decisionali o superfici personalizzati).

>[!NOTE]
>
>In questo scenario, l’evento nella parte inferiore della pagina deve attendere il completamento dell’evento nella parte superiore della pagina, per eseguire il rendering delle proposte e registrare l’evento nella parte inferiore della pagina.

```js
alloy("sendEvent", {
  xdm: { 
    ... // Optional bottom of page event data
    _experience: {
      decisioning: {
        propositions: propositions.map(function(p) {
          return {
            id: p.id,
            scope: p.scope,
            scopeDetails: p.scopeDetails
          };
        }),
        propositionEventType: {
          display: 1
        }
      }
    }
  }
});
```



| Parametro | Obbligatorio/facoltativo | Descrizione |
|---|---|---|
| `xdm._experience.decisioning.propositions` | Obbligatorio | Questa sezione definisce le proposte sottoposte a rendering manuale. Devi includere la proposta `ID`, `scope`, e `scopeDetails`. Consulta la documentazione su come [eseguire manualmente il rendering della personalizzazione](../personalization/rendering-personalization-content.md#manually) per ulteriori informazioni su come registrare eventi di visualizzazione per il contenuto sottoposto a rendering manuale. Il contenuto di personalizzazione renderizzato manualmente deve essere incluso nella parte inferiore dell’hit pagina. |
| `xdm._experience.decisioning.propositionEventType` | Obbligatorio | Imposta questo parametro su `display: 1`. |
| `xdm` | Facoltativo | Utilizza questa sezione per includere tutti i dati necessari per l’evento nella parte inferiore della pagina. |

>[!ENDTABS]


## Applicazione a pagina singola con hit nella pagina superiore e inferiore {#spa-example}


>[!BEGINTABS]

>[!TAB Visualizzazione prima pagina]

L’esempio seguente include l’aggiunta del necessario `xdm.web.webPageDetails.viewName` parametro. Questo è ciò che la rende un&#39;applicazione a pagina singola. Il `viewName` in questo esempio è la visualizzazione caricata al caricamento della pagina.

```js
// Top of page, render decisions for the "home" view.
alloy("sendEvent", {
    type: "decisioning.propositionFetch",
    renderDecisions: true,
    personalization: {
        sendDisplayEvent: false
    },
    xdm: {
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});

// Bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.

alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "home"
            }
        }
    }
});
```

>[!TAB Visualizzazione seconda pagina (opzione 1)]

In questo esempio non è necessario eseguire una divisione superiore/inferiore della pagina, perché la personalizzazione della pagina è già stata recuperata.

```js
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    ...,
    web: {
      webPageDetails: {
        viewName: "cart"
      }
    }
  }
});
```


>[!TAB Seconda visualizzazione pagina (opzione 2)]

Se devi ancora ritardare la parte inferiore dell’hit pagina, puoi utilizzare `applyPropositions` per l’hit della pagina superiore. Poiché non è necessario recuperare alcuna personalizzazione e registrare dati di Analytics, non è necessario effettuare una richiesta a Edge Network.

```js
// top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// bottom of page, send display events for the items that were rendered.
// Note: You need to include the viewName in both top and bottom of page so that the
// correct view is rendered at the top of the page, and the correct view is recorded
// at the bottom of the page.
alloy("sendEvent", {
    personalization: {
        includeRenderedPropositions: true
    },
    xdm: {
        ...,
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
});
```

>[!ENDTABS]

## Esempio GitHub {#github-sample}

Il campione trovato in [questo indirizzo](https://github.com/adobe/alloy-samples/tree/main/top-and-bottom) illustra come utilizzare Experienci Platform e Web SDK per richiedere la personalizzazione nella parte superiore della pagina e inviare le metriche di analisi nella parte inferiore. Puoi scaricare l’esempio ed eseguirlo localmente per comprendere come funzionano i primi e gli ultimi eventi di pagina.
