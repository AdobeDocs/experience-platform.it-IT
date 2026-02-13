---
title: applyPropositions
description: Riesegui il rendering delle proposte di cui è già stato eseguito il rendering con sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: e150fa51953edbb0e21de962e066deedaf8bd2d7
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# `applyPropositions`

Il comando `applyPropositions` consente di eseguire nuovamente il rendering delle proposte già sottoposte a rendering mediante il comando [`sendEvent`](sendevent/overview.md). Questo comando è utile quando si lavora con applicazioni a pagina singola in cui viene eseguito nuovamente il rendering di parti della pagina, sovrascrivendo potenzialmente eventuali personalizzazioni già applicate alla pagina.

Questo comando supporta i campi seguenti:

* **Proposte**: array di oggetti delle proposte di cui si desidera eseguire nuovamente il rendering.
* **Nome visualizzazione**: nome della visualizzazione da riprodurre. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in un comando `sendEvent` successivo utilizzando l&#39;opzione `personalization.includeRenderedPropositions`.
* **Dati Meta**: oggetto che determina la modalità di applicazione delle offerte HTML. Contiene le seguenti proprietà:
   * Portata
   * Selettore
   * Tipo di azione

>[!NOTE]
>
>Il comando `applyPropositions` non invia automaticamente eventi di visualizzazione. Se si desidera eseguire la registrazione, utilizzare il comando `sendEvent` come descritto in [Gestione eventi di visualizzazione](/help/collection/use-cases/personalization/display-events.md).

Eseguire il comando `applyPropositions` quando si chiama l&#39;istanza configurata del Web SDK. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`propositions`**: array di oggetti della proposta di cui si desidera eseguire nuovamente il rendering. Questo oggetto in genere non viene utilizzato, in quanto il campo `propositionScopes` determina in genere gli ambiti o le superfici di cui eseguire nuovamente il rendering.
* **`metadata`**: determina il modo in cui vengono applicate le offerte HTML. È una mappa in cui la chiave è un ambito o una superficie e il valore è un oggetto contenente le chiavi `selector` e `actionType`.
   * `selector`: stringa contenente un selettore CSS di dove applicare il HTML.
   * `actionType`: azione da eseguire con HTML. I valori validi includono `setHtml`, `replaceHtml` e `appendHtml`.
* **`viewName`**: nome della visualizzazione di cui eseguire il rendering in un&#39;applicazione a pagina singola. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in un comando `sendEvent` successivo utilizzando `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Applicare le proposte tramite l’estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente a questo comando è l&#39;azione [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
