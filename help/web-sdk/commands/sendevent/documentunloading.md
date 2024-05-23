---
title: documentUnloading
description: Utilizza l’API sendBeacon di JavaScript per inviare dati ad Adobe.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

Il `documentUnloading` consente di utilizzare i [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) metodo per inviare dati ad Adobe. Se una richiesta tipica richiede troppo tempo, il browser può annullarla. È possibile indicare all’SDK web di utilizzare `sendBeacon` in modo che la richiesta venga eseguita in background dopo l’uscita dalla pagina. Abilita questa proprietà per evitare che le richieste di dati vengano annullate dal browser durante lo scaricamento.

Diversi browser impongono un limite di 64 KB alla quantità di dati che può essere inviata con `sendBeacon` contemporaneamente. Se il browser rifiuta l’evento perché il payload è troppo grande, l’SDK web utilizza come fallback il normale metodo di trasporto.

## Configurare lo scaricamento del documento con l’estensione tag Web SDK

Abilita **[!UICONTROL Il documento verrà scaricato]** nelle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Abilita **[!UICONTROL Il documento verrà scaricato]** casella di controllo in [!UICONTROL Dati] sezione.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare lo scaricamento dei documenti utilizzando la libreria JavaScript dell’SDK per web

Imposta il `documentUnloading` booleano quando si esegue `sendEvent` comando. Il valore predefinito è `false`. Imposta questa proprietà su `true` se desideri utilizzare il `sendBeacon` metodo per inviare dati ad Adobe.

>[!IMPORTANT]
>
>Il `documentUnloading` è incompatibile con [`renderDecisions`](renderdecisions.md) proprietà. Non impostare entrambe le proprietà su `true` simultaneamente.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
