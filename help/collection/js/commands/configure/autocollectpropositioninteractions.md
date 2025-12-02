---
title: autoCollectPropositionInteractions
description: Raccogli automaticamente i dati quando fai clic su un collegamento.
exl-id: c70db76a-3f2f-45a6-86ab-36efcb18d20f
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# `autoCollectPropositionInteractions`

La proprietà `autoCollectPropositionInteractions` è un&#39;impostazione facoltativa che determina se il Web SDK raccoglie automaticamente le interazioni della proposta. Il valore è una mappa dei fornitori di decisioni, ciascuno con un valore che indica come devono essere gestite le interazioni automatiche della proposta.

Quando abiliti il tracciamento automatico dell’interazione della proposta, tutti i clic all’interno di un elemento della proposta sottoposto a rendering nel DOM vengono raccolti automaticamente dal Web SDK. Questa raccolta include tutte le esperienze sottoposte automaticamente a rendering nel DOM dal Web SDK e le esperienze sottoposte a rendering nel DOM utilizzando il comando [`applyPropositions`](../applypropositions.md).

Se si omette questa proprietà durante la configurazione del Web SDK, per impostazione predefinita viene utilizzato `{"AJO": "always", "TGT": "never"}`. Se preferisci non tenere traccia automaticamente delle interazioni della proposta, imposta il valore su `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "autoCollectPropositionInteractions": {
    "AJO": "always",
    "TGT": "never"
  }
});
```

Le proprietà supportate in questo oggetto includono:

| Proprietà | Descrizione |
| --- | --- |
| **`AJO`** | Adobe Journey Optimizer. |
| **`TGT`** | Adobe Target. |

I valori possibili per ciascuna proprietà includono:

| Valore | Descrizione |
| --- | --- |
| **`always`** | Raccoglie sempre automaticamente `interact` eventi per qualsiasi elemento associato a una proposta. |
| **`never`** | Non raccogliere mai automaticamente `interact` eventi per gli elementi associati a una proposta. |
| **`decoratedElementsOnly`** | Raccogli automaticamente `interact` eventi per gli elementi associati a una proposta se l&#39;elemento include attributi di dati che specificano un&#39;etichetta o un token. |

## Attributi dei dati {#data-attributes}

Puoi utilizzare gli attributi di dati sugli elementi per aggiungere specificità a un’interazione.

| Nome | Attributo dati | Descrizione |
| --- | --- | --- |
| **[!UICONTROL Label]** | `data-aep-click-label` | Quando l’attributo di dati dell’etichetta è presente su un elemento su cui è stato fatto clic, viene incluso con i dettagli di interazione inviati ad Edge Network. Il Web SDK cerca un attributo di dati di etichetta che inizia con l&#39;elemento su cui si fa clic e si sposta verso l&#39;alto nella struttura DOM. Il Web SDK utilizza la prima etichetta individuata. |
| **[!UICONTROL Token]** | `data-aep-click-token` | Usa questo token per sfruttare i criteri decisionali nelle [campagne basate su codice Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Puoi utilizzare il token per distinguere l’elemento del criterio di decisione su cui hai fatto clic. Quando l’attributo dati del token è presente su un elemento su cui è stato fatto clic, viene incluso con i dettagli di interazione inviati ad Edge Network. Il Web SDK cerca un attributo di dati token che inizi con l&#39;elemento su cui è stato fatto clic e risalga la struttura DOM. Il SDK Web utilizza il primo token trovato. |
| **[!UICONTROL Interact ID]** | `data-aep-interact-id` | Il Web SDK aggiunge automaticamente questo ID univoco agli elementi contenitore durante il rendering delle proposte. Il Web SDK utilizza questo ID per correlare gli elementi DOM alle proposte. Poiché si tratta di un ID richiesto dal Web SDK, non è necessario modificarlo in alcun modo. Puoi tranquillamente ignorarlo. |

## Esempio

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/alpha.jpg" class="poster" />
    <h2>Example Movie Alpha</h2>
    <p class="description"> A lighthearted story about exploration and friendship set on a distant world. Follow a curious rover who discovers that small actions can lead to big changes.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Alpha">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/bravo.jpg" class="poster" />
    <h2>Example Movie Bravo</h2>
    <p class="description">An uplifting tale of a determined chef who overcomes unlikely odds to create culinary masterpieces in a bustling city bistro.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Bravo">View details</button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/charlie.jpg" class="poster" />
    <h2>Example Movie Charlie</h2>
    <p class="description">A vibrant adventure following a young musician who journeys into a fantastical realm to find the true meaning of family and tradition.</p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Example-Charlie">View details</button>
    </p>
  </div>
</div>
```

### Utilizzo di `autoCollectPropositionInteractions` con il comando `applyPropositions` {#apply-propositions}

Il comando [`applyPropositions`](../applypropositions.md) è un modo pratico per eseguire il rendering delle proposte nel DOM. Tuttavia, nel caso di campagne basate su codice con JSON, puoi utilizzare questo comando per correlare un elemento DOM esistente (o quello di cui è stato eseguito il rendering del codice dell’applicazione sulla schermata in base ai valori JSON) con una proposta.

Questa correlazione attiva il tracciamento automatico delle interazioni per quell’elemento e assegna a quell’elemento la proposta appropriata. Per ottenere questo risultato, impostare `actionType` su `track`.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://example.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://example.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Configurare le interazioni di proposta automatiche per l’estensione tag Web SDK

I due menu a discesa seguenti durante la configurazione dell’estensione tag Web SDK rappresentano l’equivalente tag di questo oggetto:

* [[!UICONTROL Auto click collection for Adobe Journey Optimizer]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-journey-optimizer)
* [[!UICONTROL Auto click collection for Adobe Target]](/help/tags/extensions/client/web-sdk/configure/personalization.md#auto-click-collection-for-adobe-target)
