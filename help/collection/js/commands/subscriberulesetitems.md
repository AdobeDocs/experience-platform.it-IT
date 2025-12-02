---
title: subscribeRulesetItems
description: Sottoscrivere le schede di contenuto per una superficie specifica utilizzando il comando subscribeRulesetItems.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 3%

---

# `subscribeRulesetItems`

Il comando `subscribeRulesetItems` consente di sottoscrivere proposte che sono il risultato di set di regole soddisfatti. A tale scopo, è possibile specificare le superfici e gli schemi in base ai quali filtrare e fornire una funzione di callback.

Ogni volta che vengono valutati i set di regole, la funzione di callback riceve un oggetto `result` con una matrice di proposte al suo interno.

>[!IMPORTANT]
>
>Il comando `subscribeRulesetItems` è l&#39;unico modo per ottenere proposte provenienti da set di regole, poiché non vengono restituite insieme ai risultati di [`sendEvent`](sendevent/overview.md).


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

Il codice sopra riportato si abbona alla superficie `web://example.com/#welcome` per le schede di contenuto e utilizza il metodo di convenienza `collectEvent` per emettere `display` eventi per tutte le proposte.

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
| `collectEvent` | Funzione | Funzione di comodità che consente di inviare eventi Edge Network per monitorare interazioni, visualizzazioni e altri eventi. |

### Funzione `collectEvent` {#collectevent-function}

La funzione `collectEvent` è una funzione di convenienza che consente di inviare eventi Edge Network per tenere traccia di interazioni, visualizzazioni e altri eventi. Accetta i due parametri descritti nella tabella seguente.

| Parametro | Tipo | Descrizione |
| --- | --- | --- |
| Tipo di evento | Stringa | Stringa che indica il tipo di evento della proposta da emettere. I tipi di evento supportati sono `display`, `interact` o `dismiss`. |
| `propositions` | Array | Un array di proposte corrispondente all’evento. |

## Iscriviti alle schede di contenuto tramite l’estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente alle risposte ai comandi è una regola che sottoscrive l&#39;evento [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items). L’evento ti consente di fornire gli schemi e le superfici desiderati.
