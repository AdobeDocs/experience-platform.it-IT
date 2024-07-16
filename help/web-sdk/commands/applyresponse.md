---
title: applyResponse
description: Utilizza una risposta dell’Edge Network per inizializzare Web SDK.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

Il comando `applyResponse` consente di eseguire varie azioni in base a una risposta dell&#39;Edge Network. Viene generalmente utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale all’Edge Network. Questo comando prende la risposta da tale chiamata e inizializza l’SDK web nel browser.

## Applicare la risposta utilizzando l’estensione tag Web SDK

L’applicazione delle risposte viene eseguita come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Applica risposta]**.
1. Imposta i campi desiderati a destra.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Applicare la risposta utilizzando la libreria JavaScript dell’SDK per web

Esegui il comando `applyResponse` quando chiami l&#39;istanza configurata dell&#39;SDK Web. L’oggetto contenente le opzioni di configurazione supporta i campi seguenti:

* **`renderDecisions`**: valore booleano che forza Web SDK a eseguire il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico. Identico a [`renderDecisions`](sendevent/renderdecisions.md) nel comando [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: mappa dei nomi di intestazione stringa ai valori di intestazione stringa.
* **`responseBody`**: obbligatorio. Un corpo di risposta JSON dalla chiamata del server all’Edge Network.
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

* **`propositions`**: Array di proposte restituito dall&#39;Edge Network. Le proposte sottoposte a rendering automatico includono il flag `renderAttempted` impostato su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di machine learning su questo utente.
* **`destinations`**: Matrice di oggetti di destinazione restituita dall&#39;Edge Network.
