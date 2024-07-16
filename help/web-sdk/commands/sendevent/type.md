---
title: eventType
description: Imposta il tipo di evento per una chiamata sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

La proprietà `eventType` consente di definire il tipo di evento inviato tramite Web SDK. Questo campo alla fine popola il campo `xdm.eventType`. È utile quando desideri differenziare i tipi di evento che invii a Adobe.

In Adobe sono disponibili alcuni tipi di evento predefiniti che è possibile utilizzare. Per un elenco completo dei valori predefiniti, consulta [Valori disponibili per `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) nella guida utente di XDM. Se necessario, puoi anche utilizzare valori personalizzati.

Se imposti sia `type` qui che `xdm.eventType` nell&#39;oggetto [`xdm`](xdm.md), il valore in questo campo ha la priorità.

## Configurare il tipo di evento utilizzando l’estensione tag Web SDK

Imposta il campo a discesa **[!UICONTROL Tipo]** all&#39;interno delle azioni di una regola tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Utilizza il menu a discesa nel campo **[!UICONTROL Tipo]** oppure immetti un valore personalizzato.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare il tipo di evento utilizzando la libreria JavaScript dell’SDK Web

Impostare la proprietà stringa `eventType` durante l&#39;esecuzione del comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
