---
title: sendEvent
description: Invia dati all’Edge Network di Adobe Experience Platform.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
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
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Oggetto di risposta

Se decidi di [gestire le risposte](../command-responses.md) con questo comando, nell’oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: array di proposte restituite dall’Edge Network. Le proposte di cui viene eseguito il rendering automatico includono il flag `renderAttempted` imposta su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di apprendimento automatico su questo utente.
* **`destinations`**: array di oggetti di destinazione restituiti dall’Edge Network.
