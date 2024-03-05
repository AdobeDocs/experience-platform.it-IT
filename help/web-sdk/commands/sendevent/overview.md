---
title: sendEvent
description: Invia dati a Adobe Experience Platform Edge Network.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# `sendEvent`

Il `sendEvent` Il comando è il modo principale per inviare dati ad Adobe e recuperare contenuti, identità e destinazioni di pubblico personalizzati. Utilizza il [`xdm`](xdm.md) oggetto per inviare i dati mappati sullo schema Adobe Experience Platform. Utilizza il [`data`](data.md) oggetto per inviare dati non XDM. Puoi utilizzare il mappatore dello stream di dati per allineare i dati all’interno di questo oggetto ai campi dello schema.

## Inviare dati evento tramite l’estensione tag Web SDK

L’invio dei dati dell’evento viene eseguito come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Imposta i campi desiderati, fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Inviare dati evento utilizzando la libreria JavaScript dell’SDK per web

Esegui il `sendEvent` quando si chiama l’istanza configurata dell’SDK per web. Assicurati di chiamare il [`configure`](../configure/overview.md) prima di chiamare `sendEvent` comando.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": true,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](../command-responses.md) con questo comando, nell’oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: array di proposte restituite dalla rete Edge. Le proposte di cui viene eseguito il rendering automatico includono il flag `renderAttempted` imposta su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di apprendimento automatico su questo utente.
* **`destinations`**: array di oggetti di destinazione restituiti dalla rete Edge.
