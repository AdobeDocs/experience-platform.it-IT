---
title: applyPropositions
description: Riesegui il rendering delle proposte di cui è già stato eseguito il rendering con sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

Il `applyPropositions` consente di eseguire nuovamente il rendering delle proposte già sottoposte a rendering utilizzando [`sendEvent`](sendevent/overview.md) comando. Questo comando è utile quando si lavora con applicazioni a pagina singola in cui viene eseguito nuovamente il rendering di parti della pagina, sovrascrivendo potenzialmente eventuali personalizzazioni già applicate alla pagina.

Questo comando supporta i campi seguenti:

* **Proposte**: array di oggetti della proposta di cui desideri eseguire nuovamente il rendering.
* **Nome visualizzazione**: nome della visualizzazione da riprodurre. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in una `sendEvent` utilizzando il comando `personalization.includePendingDisplayNotifications` opzione.
* **Metadati**: oggetto che determina il modo in cui possono essere applicate le offerte HTML. Contiene le seguenti proprietà:
   * Portata
   * Selettore
   * Tipo di azione

## Applicare le proposte tramite l’estensione tag Web SDK

L’applicazione delle proposte viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Applicare le proposte]**.
1. Imposta i campi desiderati a destra.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Applicare le proposte utilizzando la libreria JavaScript dell’SDK web

Esegui il `applyPropositions` quando si chiama l’istanza configurata dell’SDK per web. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`propositions`**: array di oggetti della proposta di cui desideri eseguire nuovamente il rendering. Questo oggetto in genere non viene utilizzato, in quanto `propositionScopes` in genere determina gli ambiti o le superfici di cui eseguire nuovamente il rendering.
* **`metadata`**: determina il modo in cui vengono applicate le offerte HTML. È una mappa in cui la chiave è un ambito o una superficie e il valore è un oggetto contenente le chiavi `selector` e `actionType`.
   * `selector`: stringa contenente un selettore CSS di dove applicare il HTML.
   * `actionType`: azione da intraprendere con il HTML. I valori validi includono `setHtml`, `replaceHtml` e `appendHtml`.
* **`viewName`**: nome della visualizzazione da riprodurre in un’applicazione a pagina singola. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in una `sendEvent` comando tramite `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
