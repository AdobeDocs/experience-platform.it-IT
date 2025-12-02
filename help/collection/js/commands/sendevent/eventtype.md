---
title: eventType
description: Imposta il tipo di evento per una chiamata sendEvent.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

La proprietà `eventType` consente di definire il tipo di evento inviato tramite Web SDK. Questo campo alla fine popola il campo `xdm.eventType`. È utile quando desideri differenziare i tipi di evento inviati ad Adobe.

Adobe fornisce alcuni tipi di evento predefiniti che è possibile utilizzare. Per un elenco completo dei valori predefiniti, consulta [Valori disponibili per `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) nella guida utente di XDM. Se necessario, puoi anche utilizzare valori personalizzati.

Se imposti sia `type` qui che `xdm.eventType` nell&#39;oggetto [`xdm`](xdm.md), il valore in questo campo ha la priorità.

Impostare la proprietà stringa `eventType` durante l&#39;esecuzione del comando `sendEvent`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Tipo di evento con l’estensione tag Web SDK

L&#39;equivalente dell&#39;estensione tag Web SDK di questa proprietà è il menu a discesa [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) durante la configurazione di un&#39;azione &#39;[!UICONTROL Send event]&#39;.
