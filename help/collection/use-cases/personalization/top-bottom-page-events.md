---
title: Configurare gli eventi di inizio e fine pagina in Web SDK
description: Questo articolo spiega come utilizzare la parte superiore e inferiore degli eventi di pagina in Web SDK.
exl-id: 43c6d53a-6bf9-45f8-b001-d148adaff829
source-git-commit: 8058ee470717b95d30269a8072b12385c920c85f
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 1%

---


# Configurare gli eventi di inizio e fine pagina in Web SDK

Quando fornisci esperienze personalizzate, il tempo di caricamento di una pagina web è essenziale. Per ridurre al minimo il tempo di attesa di contenuti personalizzati da parte di un utente, Web SDK supporta la configurazione degli eventi di inizio e fine pagina.

La parte superiore e inferiore degli eventi di pagina descrivono un metodo per caricare in modo asincrono vari elementi nella pagina mantenendo al minimo il tempo di caricamento della pagina:

* La parte superiore dell’evento pagina richiede la personalizzazione non appena la pagina inizia a caricarsi.
* La parte inferiore dell’evento di pagina registra la visualizzazione di una pagina al termine del caricamento.

Adobe Analytics ignora gli eventi di inizio pagina, il che porta a una registrazione più accurata delle metriche, in quanto viene registrato un solo hit pagina (la parte inferiore dell’evento pagina).

È possibile configurare gli eventi di inizio e fine pagina in due modi: chiamando direttamente la libreria Web SDK JavaScript (`alloy()`) oppure utilizzando l&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag di Adobe Experience Platform. L&#39;azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) dell&#39;estensione tag include un&#39;opzione &#39;[!UICONTROL Use guided events]&#39; che preconfigura i valori dei campi per gli scenari &#39;[!UICONTROL Request personalization]&#39; (inizio pagina) e &#39;[!UICONTROL Collect analytics]&#39; (fine pagina). Ogni esempio seguente mostra entrambe le implementazioni.

## Evento all’inizio della pagina {#top-of-page}

L&#39;esempio seguente configura un evento all&#39;inizio della pagina che richiede la personalizzazione ma elimina [eventi di visualizzazione](display-events.md) per le proposte sottoposte a rendering automatico. Tali eventi di visualizzazione vengono invece inviati con la parte inferiore dell’evento pagina.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

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
| --- | --- | --- |
| `type` | Obbligatorio | Imposta questo parametro su `decisioning.propositionFetch`. Questo tipo di evento speciale comunica ad Adobe Analytics di eliminare questo evento. Quando utilizzi Customer Journey Analytics, puoi anche impostare un filtro per eliminare questi eventi. Per ulteriori informazioni, vedere [Tipi di evento Edge Network in Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/hit-types). |
| `renderDecisions` | Obbligatorio | Imposta questo parametro su `true`. Questo parametro indica a Web SDK di eseguire il rendering delle decisioni restituite da Edge Network. |
| `personalization.sendDisplayEvent` | Obbligatorio | Imposta questo parametro su `false`. Questo parametro interrompe l’invio degli eventi di visualizzazione. |

>[!TAB Estensione tag Web SDK]

Configura un&#39;azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) nella regola che viene attivata nella parte superiore della pagina. Abilita **[!UICONTROL Use guided events]**, quindi seleziona **[!UICONTROL Request personalization]**. Questa opzione blocca &#39;[!UICONTROL Type]&#39; in &#39;[!UICONTROL Decisioning Proposition Fetch]&#39;, &#39;[!UICONTROL Render visual personalization decisions]&#39; in abilitato e &#39;[!UICONTROL Automatically send a display event]&#39; in disabilitato.

Per impostare questi campi manualmente, lasciare disabilitato **[!UICONTROL Use guided events]** e configurare ogni campo manualmente.

>[!ENDTABS]

## Esempi di eventi nella parte inferiore della pagina {#bottom-of-page}

### Proposizioni con rendering automatico {#bottom-auto-rendered}

L&#39;esempio seguente configura un evento in fondo alla pagina che invia eventi di visualizzazione per le proposte di cui è stato eseguito il rendering automatico nella pagina ma che sono state eliminate nell&#39;evento [superiore alla pagina](#top-of-page).

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

```js
alloy("sendEvent", {
  personalization: {
    includeRenderedPropositions: true
  },
  xdm: { ... }
});
```

| Parametro | Obbligatorio/facoltativo | Descrizione |
| --- | --- | --- |
| `personalization.includeRenderedPropositions` | Obbligatorio | Imposta questo parametro su `true`. Questo parametro consente l’invio di eventi di visualizzazione soppressi nella parte superiore dell’evento pagina. |
| `xdm` | Facoltativo | Utilizzare questo oggetto per includere tutti i dati desiderati per l&#39;evento di fine pagina. |

>[!TAB Estensione tag Web SDK]

Configura un&#39;azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) nella regola che viene attivata nella parte inferiore della pagina. Abilita **[!UICONTROL Use guided events]**, quindi seleziona **[!UICONTROL Collect analytics]**. Questa opzione blocca &#39;[!UICONTROL Include rendered propositions]&#39; su abilitato.

Per impostare questo campo manualmente, lasciare disabilitato **[!UICONTROL Use guided events]** e abilitare direttamente **[!UICONTROL Include rendered propositions]**. Facoltativamente, compila il campo **[!UICONTROL XDM]** con un elemento dati [oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) che trasporta i dati della pagina.

>[!ENDTABS]

### Proposizioni sottoposte a rendering manuale {#bottom-manually-rendered}

L’esempio seguente configura un evento nella parte inferiore della pagina che invia eventi di visualizzazione per le proposte di cui è stato eseguito il rendering manuale sulla pagina (ovvero, per ambiti decisionali o superfici personalizzati).

>[!NOTE]
>
>In questo scenario, l’evento nella parte inferiore della pagina deve attendere il completamento dell’evento nella parte superiore della pagina, in modo da poter eseguire il rendering e registrare le proposte.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

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
| --- | --- | --- |
| `xdm._experience.decisioning.propositions` | Obbligatorio | Questa sezione definisce le proposte sottoposte a rendering manuale. È necessario includere la proposta `id`, `scope` e `scopeDetails`. Per ulteriori informazioni, vedere [Gestione eventi di visualizzazione](display-events.md). Il contenuto di personalizzazione renderizzato manualmente deve essere incluso nella parte inferiore dell’evento pagina. |
| `xdm._experience.decisioning.propositionEventType` | Obbligatorio | Imposta questo parametro su `display: 1`. |
| `xdm` | Facoltativo | Utilizzare questo oggetto per includere tutti i dati desiderati per l&#39;evento di fine pagina. |

>[!TAB Estensione tag Web SDK]

L&#39;opzione &#39;[!UICONTROL Use guided events]&#39; non copre lo scenario, pertanto configurare l&#39;azione manualmente:

1. Crea un elemento dati [oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) (o [Variabile](/help/tags/extensions/client/web-sdk/data-element-types.md#variable)) che popola `_experience.decisioning.propositions` con ogni proposta di cui è stato eseguito il rendering `id`, `scope` e `scopeDetails` e imposta `_experience.decisioning.propositionEventType.display` su `1`. Per ulteriori informazioni, vedere [Gestione eventi di visualizzazione](display-events.md).
1. Nell&#39;azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md) per la parte inferiore della regola di pagina, lascia disabilitato **[!UICONTROL Use guided events]** e fai riferimento all&#39;elemento dati dal campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Applicazione a pagina singola con eventi nella parte superiore e inferiore della pagina {#spa-example}

In un&#39;applicazione a pagina singola è necessario specificare il nome della visualizzazione per ogni modifica della visualizzazione in modo che Web SDK esegua il rendering della personalizzazione corretta nella parte superiore della pagina e registri la visualizzazione corretta nella parte inferiore della pagina.

### Visualizzazione prima pagina {#spa-first-view}

In questo esempio, `home` è la visualizzazione caricata al caricamento della pagina iniziale.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

La chiamata superiore richiede la personalizzazione per la visualizzazione `home` senza registrare un hit di Analytics o attivare eventi di visualizzazione. La chiamata in basso registra la visualizzazione della pagina e attiva gli eventi di visualizzazione soppressi. Includere lo stesso `viewName` in entrambe le chiamate in modo che la visualizzazione venga registrata in modo coerente.

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

>[!TAB Estensione tag Web SDK]

1. Creare un elemento dati [oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) che imposta `web.webPageDetails.viewName` sul nome della visualizzazione (ad esempio, `home`).
1. Configura un&#39;azione nella parte superiore della pagina [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): abilita **[!UICONTROL Use guided events]**, seleziona **[!UICONTROL Request personalization]** e fai riferimento all&#39;elemento dati nel campo **[!UICONTROL XDM]**.
1. Configura un&#39;azione nella parte inferiore della pagina **[!UICONTROL Send event]**: abilita **[!UICONTROL Use guided events]**, seleziona **[!UICONTROL Collect analytics]** e fai riferimento allo stesso elemento dati nel campo **[!UICONTROL XDM]** in modo che `viewName` corrisponda in entrambi gli eventi.

>[!ENDTABS]

### Seconda visualizzazione pagina — opzione 1 {#spa-second-view-option-1}

In questo esempio, un singolo evento è sufficiente perché la personalizzazione della pagina è già stata recuperata.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

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

>[!TAB Estensione tag Web SDK]

1. Creare un elemento dati [oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) che imposta `web.webPageDetails.viewName` sul nome della nuova visualizzazione (ad esempio, `cart`).
1. Alla modifica della visualizzazione, configurare una singola azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): lasciare disabilitato **[!UICONTROL Use guided events]**, abilitare **[!UICONTROL Render visual personalization decisions]** e fare riferimento all&#39;elemento dati nel campo **[!UICONTROL XDM]**.

>[!ENDTABS]

### Seconda visualizzazione pagina — opzione 2 {#spa-second-view-option-2}

Utilizza questo approccio quando devi ritardare l’evento nella parte inferiore della pagina (ad esempio, quando i dati di analisi della pagina non sono pronti al momento della modifica della visualizzazione). La modifica della visualizzazione può essere gestita in due passaggi:

1. Nella parte superiore della pagina, esegui il rendering delle proposte già recuperate senza effettuare una chiamata Edge Network.
1. Una volta che i dati di analisi sono pronti, invia il fondo della pagina dell’evento.

Includere lo stesso `viewName` in entrambe le chiamate in modo che la visualizzazione venga registrata in modo coerente.

>[!BEGINTABS]

>[!TAB Libreria JavaScript]

Chiamare [`applyPropositions`](/help/collection/js/commands/applypropositions.md) nella parte superiore della pagina per eseguire il rendering delle proposte memorizzate nella cache per la nuova visualizzazione. Quindi chiama `sendEvent` nella parte inferiore della pagina con `includeRenderedPropositions: true` in modo che gli eventi di visualizzazione soppressi si attivino.

```js
// Top of page, render the decisions already fetched for the "cart" view.
alloy("applyPropositions", {
    viewName: "cart"
});

// Bottom of page, send display events for the items that were rendered.
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

>[!TAB Estensione tag Web SDK]

1. Creare un elemento dati [oggetto XDM](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) che imposta `web.webPageDetails.viewName` sul nome della nuova visualizzazione (ad esempio, `cart`).
1. Per l&#39;evento all&#39;inizio della pagina, configurare un&#39;azione [[!UICONTROL Apply propositions]](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) e impostare il campo **[!UICONTROL View name]** sul nome della visualizzazione, ad esempio `cart`. Questa azione esegue il rendering delle proposte già recuperate senza contattare Edge Network.
1. Per l&#39;evento nella parte inferiore della pagina, configurare un&#39;azione [[!UICONTROL Send event]](/help/tags/extensions/client/web-sdk/actions/send-event.md): abilita **[!UICONTROL Use guided events]**, seleziona **[!UICONTROL Collect analytics]** e fai riferimento all&#39;elemento dati nel campo **[!UICONTROL XDM]**.

>[!ENDTABS]

## Esempio GitHub {#github-sample}

Il [esempio dall&#39;alto verso il basso nell&#39;archivio dei campioni di lega](https://github.com/adobe/alloy-samples/tree/main/target/top-and-bottom) illustra come richiedere la personalizzazione nella parte superiore della pagina e inviare le metriche di analisi nella parte inferiore. Scarica l’esempio ed eseguilo localmente per vedere come funzionano la parte superiore e inferiore degli eventi di pagina. Nell&#39;esempio viene utilizzata direttamente la libreria JavaScript; gli stessi pattern vengono applicati quando si configurano regole equivalenti nell&#39;estensione tag Web SDK.
