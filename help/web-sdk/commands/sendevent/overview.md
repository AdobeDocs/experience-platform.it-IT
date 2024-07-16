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

Il comando `sendEvent` è il modo principale per inviare dati ad Adobe e recuperare contenuti, identità e destinazioni di pubblico personalizzati. Utilizzare l&#39;oggetto [`xdm`](xdm.md) per inviare i dati mappati allo schema Adobe Experience Platform. Utilizzare l&#39;oggetto [`data`](data.md) per inviare dati non XDM. Puoi utilizzare il mappatore dello stream di dati per allineare i dati all’interno di questo oggetto ai campi dello schema.

## Inviare dati evento tramite l’estensione tag Web SDK

L’invio dei dati dell’evento viene eseguito come azione all’interno di una regola nell’interfaccia dei tag di Adobe Experience Platform Data Collection.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Imposta i campi desiderati, fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Inviare dati evento tramite la libreria JavaScript dell’SDK per web

Esegui il comando `sendEvent` quando chiami l&#39;istanza configurata dell&#39;SDK Web. Assicurarsi di chiamare il comando [`configure`](../configure/overview.md) prima di chiamare il comando `sendEvent`.

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

Se decidi di [gestire le risposte](../command-responses.md) con questo comando, nell&#39;oggetto di risposta sono disponibili le seguenti proprietà:

* **`propositions`**: Array di proposte restituito dall&#39;Edge Network. Le proposte sottoposte a rendering automatico includono il flag `renderAttempted` impostato su `true`.
* **`inferences`**: array di oggetti di inferenza che contengono informazioni di machine learning su questo utente.
* **`destinations`**: Matrice di oggetti di destinazione restituita dall&#39;Edge Network.
