---
title: applyResponse
description: Utilizza una risposta di Edge Network per inizializzare Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

Il comando `applyResponse` consente di eseguire varie azioni in base a una risposta di Edge Network. Viene generalmente utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale ad Edge Network. Questo comando prende la risposta da tale chiamata e inizializza il Web SDK nel browser.

Eseguire il comando `applyResponse` quando si chiama l&#39;istanza configurata del Web SDK. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`renderDecisions`**: valore booleano che forza il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico in Web SDK. Identico a [`renderDecisions`](sendevent/renderdecisions.md) nel comando [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: mappa dei nomi di intestazione stringa ai valori di intestazione stringa.
* **`responseBody`**: obbligatorio. Un corpo di risposta JSON dalla chiamata del server ad Edge Network.
* **`personalization.sendDisplayEvent`**: valore booleano che funziona in modo identico a [`personalization.sendDisplayEvent`](sendevent/personalization.md) nel comando `sendEvent`.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: array di proposte restituito da Edge Network. Le proposte sottoposte a rendering automatico includono il flag `renderAttempted` impostato su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di machine learning su questo utente.
* **`destinations`**: array di oggetti di destinazione restituiti da Edge Network.

## Applicare la risposta utilizzando l’estensione tag Web SDK

L&#39;estensione tag Web SDK equivalente a questo comando è l&#39;azione [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).
