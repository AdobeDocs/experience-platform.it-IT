---
title: sendEvent
description: Invia dati a Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

Il comando `sendEvent` è il modo principale per inviare dati ad Adobe. Il relativo oggetto di risposta è il modo principale per recuperare contenuti personalizzati, identità e destinazioni di pubblico. Utilizzare l&#39;oggetto [`xdm`](xdm.md) per inviare i dati mappati allo schema Adobe Experience Platform. Utilizzare l&#39;oggetto [`data`](data.md) per inviare dati non XDM. Il payload durante l’invio di dati ad Adobe ha un limite massimo di 64 KB.

Eseguire il comando `sendEvent` quando si chiama l&#39;istanza configurata del Web SDK. Assicurarsi di chiamare il comando [`configure`](../configure/overview.md) prima di chiamare il comando `sendEvent`.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](../command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: array di proposte restituito da Edge Network. Le proposte sottoposte a rendering automatico includono il flag `renderAttempted` impostato su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di machine learning su questo utente.
* **`destinations`**: array di oggetti di destinazione restituiti da Edge Network.

## Inviare un evento tramite l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questo comando è l&#39;azione [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).
