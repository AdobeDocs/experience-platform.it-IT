---
title: autoTrackPropositionInteractionsEnabled
description: Scopri come configurare Experience Platform Web SDK per la raccolta automatica dei dati di collegamento.
source-git-commit: ec5fd1c8228388ced96f58476e0174c8a0ff00df
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---


# `autoTrackPropositionInteractionsEnabled`

La proprietà `autoTrackPropositionInteractionsEnabled` è un&#39;impostazione facoltativa che determina se Web SDK deve raccogliere automaticamente le interazioni della proposta.

Il valore è una mappa dei fornitori di decisioni, ciascuno con un valore che indica come devono essere gestite le interazioni automatiche della proposta.

## Valori supportati {#supported-values}

Per impostazione predefinita, le interazioni di proposta automatiche sono _sempre_ raccolte per Adobe Journey Optimizer (`AJO`) e _mai_ raccolte per Adobe Target (`TGT`).

Il valore predefinito di `autoTrackPropositionInteractions` è mostrato di seguito.

```json
{
  "AJO": "always",
  "TGT": "never"
}
```

Fai riferimento alla tabella seguente per i valori di configurazione supportati per ciascun provider di decisioni.

| Valore | Descrizione |
| --- | --- |
| `always` | [!DNL Web SDK] raccoglierà sempre automaticamente `interact` eventi per tutti gli elementi associati a una proposta. |
| `never` | [!DNL Web SDK] non raccoglierà mai automaticamente `interact` eventi per gli elementi associati a una proposta. |
| `decoratedElementsOnly` | [!DNL Web SDK] raccoglierà automaticamente `interact` eventi per gli elementi associati a una proposta, ma solo se l&#39;elemento include attributi di dati che specificano un&#39;etichetta o un token. |

## Tracciamento automatico delle interazioni delle proposte {#logic}

Quando abiliti il tracciamento automatico dell&#39;interazione della proposta, tutti i clic all&#39;interno di un elemento della proposta sottoposto a rendering nel DOM verranno raccolti automaticamente da [!DNL Web SDK]. Sono incluse tutte le esperienze sottoposte a rendering automatico nel DOM da [!DNL Web SDK] e le esperienze sottoposte a rendering nel DOM utilizzando il comando [`applyPropositions`](../applypropositions.md).

### Attributi dei dati {#data-attributes}

Puoi utilizzare gli attributi di dati sugli elementi per aggiungere specificità a un’interazione.

| Nome | Attributo dati | Descrizione |
| --- | --- | --- |
| [!DNL Label] | `data-aep-click-label` | Quando l&#39;attributo di dati dell&#39;etichetta è presente in un elemento su cui è stato fatto clic, viene incluso nei dettagli di interazione inviati a [!DNL Edge Network]. [!DNL Web SDK] cerca un attributo di dati di etichetta che inizia con l&#39;elemento su cui si fa clic e si sposta verso l&#39;alto nella struttura DOM. [!DNL Web SDK] utilizza la prima etichetta trovata. |
| [!DNL Token] | `data-aep-click-token` | Usa questo token per sfruttare i criteri decisionali nelle [campagne basate su codice Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based). Puoi utilizzare il token per distinguere l’elemento del criterio di decisione su cui hai fatto clic. Quando l’attributo dei dati del token è presente su un elemento su cui è stato fatto clic, viene incluso con i dettagli di interazione inviati all’Edge Network. [!DNL Web SDK] cerca un attributo di dati token che inizia con l&#39;elemento su cui è stato fatto clic e che si sposta verso l&#39;alto nella struttura DOM. [!DNL Web SDK] utilizza il primo token trovato. |
| [!DNL Interact ID] | `data-aep-interact-id` | [!DNL Web SDK] aggiunge automaticamente questo ID univoco agli elementi contenitore durante il rendering delle proposte. Web SDK utilizza questo ID per correlare [!DNL DOM] elementi con le proposte. Poiché si tratta di un ID richiesto da [!DNL Web SDK], non modificarlo in alcun modo. Puoi tranquillamente ignorarlo. |

**Esempio**

Fai riferimento al frammento di codice seguente per visualizzare un esempio di utilizzo degli attributi di dati.

```html
<div class="row movies" data-aep-interact-id="5">
  <div class="col-md-4 movie" data-aep-click-token="wlpk/z/qyDGoFGF1E47O0w">
    <img src="/img/walle.jpg" class="poster" />
    <h2>WALL·E</h2>
    <p class="description"> In a distant, but not so unrealistic, future where mankind has abandoned earth because it has become covered with trash from products sold by the powerful multi-national Buy N Large corporation, WALL-E, a garbage collecting robot has been left to clean up the mess. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-WALL·E"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="6ZUrou9BVKIsINIAqxylzw">
    <img src="/img/ratatouille.jpg" class="poster" />
    <h2>Ratatouille</h2>
    <p class="description"> A rat named Remy dreams of becoming a great French chef despite his family's wishes and the obvious problem of being a rat in a decidedly rodent-phobic profession. When fate places Remy in the sewers of Paris, he finds himself ideally situated beneath a restaurant made famous by his culinary hero, Auguste Gusteau. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Ratatouille"> View details >> </button>
    </p>
  </div>
  <div class="col-md-4 movie" data-aep-click-token="QuuXntMRGnCP/AsZHf4pnQ">
    <img src="/img/coco.jpg" class="poster" />
    <h2>Coco</h2>
    <p class="description"> Despite his family's baffling generations-old ban on music, Miguel dreams of becoming an accomplished musician like his idol, Ernesto de la Cruz. Desperate to prove his talent, Miguel finds himself in the stunning and colorful Land of the Dead following a mysterious chain of events. </p>
    <p>
      <button class="btn btn-default" data-aep-click-label="view-movie-Coco"> View details >> </button>
    </p>
  </div>
</div>
```

### Il comando `applyPropositions` {#apply-propositions}

Per informazioni sul funzionamento di questo comando, consultare la documentazione di [`applyPropositions`](../applypropositions.md).

Il comando `applyPropositions` è un modo pratico per eseguire il rendering delle proposte in [!DNL DOM]. Tuttavia, nel caso di campagne basate su codice con `JSON`, puoi utilizzare questo comando per correlare un elemento [!DNL DOM] esistente (o quello di cui il codice dell&#39;applicazione ha eseguito il rendering sullo schermo in base ai valori `JSON`) con una proposta.

Questa correlazione attiva il tracciamento automatico delle interazioni per quell’elemento e assegna a quell’elemento la proposta appropriata. Per ottenere questo risultato, impostare `actionType` su `track`.

**Esempio**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
}).then((result) => {
    const {
        propositions = []
    } = result;
    const proposition = propositions.find(
        (proposition) => proposition.scope === "web://mywebsite.com/#weather-widget"
    );

    if (proposition) {
        renderWeatherWidget(proposition); // custom code that renders the weather widget based on the code-based campaign JSON

        alloy("applyPropositions", {
            propositions: [proposition],
            metadata: {
                "web://mywebsite.com/#weather-widget": {
                    selector: "#weather-widget",
                    actionType: "track",
                },
            },
        });
    }
});
```

## Abilitare il tracciamento automatico delle proposte e delle interazioni tramite clic attraverso l’estensione tag Web SDK {#tag-extension}

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le tue credenziali Adobe ID.
2. Passa a **Raccolta dati** > **Tag**.
3. Seleziona la proprietà tag desiderata.
4. Passa a **Estensioni**, quindi seleziona **Configura** nella scheda Adobe Experience Platform Web SDK.
5. Scorri verso il basso fino alla sezione **[!UICONTROL Raccolta dati]**, quindi seleziona la casella di controllo **Abilita proposte e tracciamento collegamenti di interazione**.
6. Seleziona **Salva**, quindi pubblica le modifiche.

## Abilitare il tracciamento automatico dei collegamenti di proposte e interazioni tramite la libreria JavaScript dell’SDK per web {#library}

Il tracciamento delle proposte è abilitato per impostazione predefinita in [!DNL Web SDK]. Tuttavia, è possibile configurarlo ulteriormente utilizzando il valore `autoTrackPropositionInteractionsEnabled` durante l&#39;esecuzione del comando [`configure`](../configure/overview.md).

Se si omette questa proprietà durante la configurazione dell&#39;SDK Web, per impostazione predefinita verrà utilizzato `{"AJO": "always", "TGT": "never"}`. Se preferisci non tenere traccia automaticamente delle interazioni della proposta, imposta il valore su `{"AJO": "never", "TGT": "never"}`.

```javascript
alloy("configure", {
   "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
   "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
   "autoTrackPropositionInteractionsEnabled": {"AJO": "always", "TGT": "never"}
});
```
