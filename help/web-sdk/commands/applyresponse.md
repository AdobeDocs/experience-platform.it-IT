---
title: applyResponse
description: Utilizza una risposta di Edge Network per inizializzare Web SDK.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

Il `applyResponse` consente di eseguire varie azioni in base a una risposta della rete Edge. In genere viene utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale alla rete Edge. Questo comando prende la risposta da tale chiamata e inizializza l’SDK web nel browser.

## Applicare la risposta utilizzando l’estensione tag Web SDK

L’applicazione delle risposte viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Applica risposta]**.
1. Imposta i campi desiderati a destra.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Applicare la risposta utilizzando la libreria JavaScript dell’SDK per web

Esegui il `applyResponse` quando si chiama l’istanza configurata dell’SDK per web. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`renderDecisions`**: valore booleano che forza il Web SDK a eseguire il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico. Identico a [`renderDecisions`](sendevent/renderdecisions.md) nel [`sendEvent`](sendevent/overview.md) comando.
* **`responseHeaders`**: mappa dei nomi di intestazione stringa ai valori di intestazione stringa.
* **`responseBody`**: obbligatorio. Un corpo di risposta JSON dalla chiamata del server alla rete Edge.
* **`personalization.sendDisplayEvent`**: valore booleano che funziona in modo identico a [`personalization.sendDisplayEvent`](sendevent/personalization.md) nel `sendEvent` comando.

```js
allow("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](command-responses.md) con questo comando, nell’oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: array di proposte restituite dalla rete Edge. Le proposte di cui viene eseguito il rendering automatico includono il flag `renderAttempted` imposta su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di apprendimento automatico su questo utente.
* **`destinations`**: array di oggetti di destinazione restituiti dalla rete Edge.
