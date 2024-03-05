---
title: eventType
description: Imposta il tipo di evento per una chiamata sendEvent.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

Il `eventType` consente di definire il tipo di evento inviato tramite Web SDK. Questo campo alla fine popola il `xdm.eventType` campo. È utile quando desideri differenziare i tipi di evento che invii a Adobe.

In Adobe sono disponibili alcuni tipi di evento predefiniti che è possibile utilizzare. Consulta [Valori disponibili per `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) nella guida utente di XDM per un elenco completo dei valori predefiniti. Se necessario, puoi anche utilizzare valori personalizzati.

Se si impostano entrambi `type` qui e `xdm.eventType` nel [`xdm`](xdm.md) , il valore in questo campo ha la priorità.

## Configurare il tipo di evento utilizzando l’estensione tag Web SDK

Imposta il **[!UICONTROL Tipo]** campo a discesa all’interno delle azioni di una regola tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Utilizza il menu a discesa sotto **[!UICONTROL Tipo]** o immettere un valore personalizzato.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare il tipo di evento utilizzando la libreria JavaScript dell’SDK Web

Imposta il `eventType` proprietà stringa durante l&#39;esecuzione di `sendEvent` comando.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
