---
title: subscribeRulesetItems
description: Sottoscrivere le schede di contenuto per una superficie specifica utilizzando il comando subscribeRulesetItems.
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

Il comando `subscribeRulesetItems` consente di sottoscrivere proposte che sono il risultato di set di regole soddisfatti. A tale scopo, è possibile specificare le superfici e gli schemi in base ai quali filtrare e fornire una funzione di callback.

Ogni volta che vengono valutati i set di regole, la funzione di callback riceve un oggetto `result` con una matrice di proposte al suo interno.

>[!IMPORTANT]
>
>Il comando `subscribeRulesetItems` è l&#39;unico modo per ottenere proposte provenienti da set di regole, poiché non vengono restituite insieme ai risultati di [`sendEvent`](sendevent/overview.md).

## Opzioni comando {#command-options}

Questo comando accetta un oggetto `options` con le seguenti proprietà:

| Proprietà | Tipo | Descrizione |
| --- | --- | --- |
| `surfaces` | Array di stringhe | Un elenco di superfici. Le proposte verranno ricevute dalla funzione di callback solo se corrispondono a una delle superfici fornite qui. |
| `schemas` | Array di stringhe | Elenco di schemi. Le proposte verranno ricevute dalla funzione di callback solo se corrispondono a uno degli schemi forniti qui. |
| `callback` | Funzione | Funzione di callback che verrà richiamata quando le proposte sono il risultato di set di regole soddisfatti. La funzione di callback riceve due parametri quando richiamata: `result` e `collectEvent`. Per ulteriori dettagli, vedere [parametri di callback](#callback-parameters). |

### Parametri di callback {#callback-parameters}

Quando viene richiamata, la funzione di callback riceve i due parametri descritti nella tabella seguente.

| Parametro | Tipo | Descrizione |
| --- | --- | --- |
| `result` | Oggetto | Questo oggetto contiene un array `propositions`.  Queste proposte sono il risultato diretto di set di regole soddisfatti. L&#39;oggetto `result` è strutturato come l&#39;[oggetto risultato](command-responses.md) restituito da `sendEvent` tramite una clausola `then`. |
| `collectEvent` | Funzione | Funzione di comodità che consente di inviare eventi di Edge Network per tenere traccia di interazioni, visualizzazioni e altri eventi. |

### Funzione `collectEvent` {#collectevent-function}

La funzione `collectEvent` è una funzione di convenienza che consente di inviare eventi di Edge Network per tenere traccia di interazioni, visualizzazioni e altri eventi. Accetta i due parametri descritti nella tabella seguente.

| Parametro | Tipo | Descrizione |
| --- | --- | --- |
| Tipo di evento | Stringa | Stringa che indica il tipo di evento della proposta da emettere. I tipi di evento supportati sono `display`, `interact` o `dismiss`. |
| `propositions` | Array | Un array di proposte corrispondente all’evento. |

## Iscriviti alle schede di contenuto tramite l’estensione tag Web SDK {#tag-extension}

Segui i passaggi seguenti per iscriverti alle schede di contenuti tramite l’interfaccia utente Tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Eventi], seleziona un evento esistente o creane uno nuovo.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta **[!UICONTROL Tipo evento]** su **[!UICONTROL Sottoscrivi elementi set di regole]**.
1. Sul lato destro dello schermo, seleziona gli schemi e le superfici per i quali desideri iscriverti alle schede di contenuto.
1. Seleziona **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Iscriviti alle schede di contenuto utilizzando la libreria JavaScript dell’SDK per web {#library}

Il codice di esempio seguente si abbona alla superficie `web://mywebsite.com/#welcome` per le schede di contenuto e utilizza il metodo di convenienza `collectEvent` per emettere `display` eventi per tutte le proposte.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
