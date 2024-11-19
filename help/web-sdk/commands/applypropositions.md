---
title: applyPropositions
description: Riesegui il rendering delle proposte di cui è già stato eseguito il rendering con sendEvent.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

Il comando `applyPropositions` consente di eseguire nuovamente il rendering delle proposte già sottoposte a rendering mediante il comando [`sendEvent`](sendevent/overview.md). Questo comando è utile quando si lavora con applicazioni a pagina singola in cui viene eseguito nuovamente il rendering di parti della pagina, sovrascrivendo potenzialmente eventuali personalizzazioni già applicate alla pagina.

Questo comando supporta i campi seguenti:

* **Proposte**: array di oggetti delle proposte di cui si desidera eseguire nuovamente il rendering.
* **Nome visualizzazione**: nome della visualizzazione da riprodurre. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in un comando `sendEvent` successivo utilizzando l&#39;opzione `personalization.includeRenderedPropositions`.
* **Metadati**: oggetto che determina la modalità di applicazione delle offerte HTML. Contiene le seguenti proprietà:
   * Portata
   * Selettore
   * Tipo di azione

## Applicare le proposte tramite l’estensione tag Web SDK

L’applicazione delle proposte viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Applica proposte]**.
1. Imposta i campi desiderati a destra.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Applicare le proposte utilizzando la libreria JavaScript dell’SDK web

Esegui il comando `applyPropositions` quando chiami l&#39;istanza configurata dell&#39;SDK Web. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`propositions`**: array di oggetti della proposta di cui si desidera eseguire nuovamente il rendering. Questo oggetto in genere non viene utilizzato, in quanto il campo `propositionScopes` determina in genere gli ambiti o le superfici di cui eseguire nuovamente il rendering.
* **`metadata`**: determina il modo in cui vengono applicate le offerte HTML. È una mappa in cui la chiave è un ambito o una superficie e il valore è un oggetto contenente le chiavi `selector` e `actionType`.
   * `selector`: stringa contenente un selettore CSS di dove applicare il HTML.
   * `actionType`: azione da eseguire con il HTML. I valori validi includono `setHtml`, `replaceHtml` e `appendHtml`.
* **`viewName`**: nome della visualizzazione di cui eseguire il rendering in un&#39;applicazione a pagina singola. Le notifiche di visualizzazione per queste decisioni sono memorizzate nella cache e possono essere incluse in un comando `sendEvent` successivo utilizzando `personalization.includeRenderedPropositions`.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
