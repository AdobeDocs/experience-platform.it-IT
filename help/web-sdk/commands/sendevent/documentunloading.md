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

La proprietà `documentUnloading` consente di utilizzare il metodo [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) di JavaScript per inviare dati ad Adobe. Se una richiesta tipica richiede troppo tempo, il browser può annullarla. È possibile indicare all&#39;SDK Web di utilizzare `sendBeacon` in modo che la richiesta venga eseguita in background dopo l&#39;uscita dalla pagina. Abilita questa proprietà per evitare che le richieste di dati vengano annullate dal browser durante lo scaricamento.

Diversi browser impongono un limite di 64 KB alla quantità di dati che è possibile inviare contemporaneamente con `sendBeacon`. Se il browser rifiuta l’evento perché il payload è troppo grande, l’SDK web utilizza come fallback il normale metodo di trasporto.

## Configurare lo scaricamento del documento con l’estensione tag Web SDK

Abilita la casella di controllo **[!UICONTROL Documento verrà scaricato]** nelle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Abilita la casella di controllo **[!UICONTROL Documento verrà scaricato]** nella sezione [!UICONTROL Dati].
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Configurare lo scaricamento dei documenti utilizzando la libreria JavaScript dell’SDK per web

Impostare il valore booleano `documentUnloading` durante l&#39;esecuzione del comando `sendEvent`. Il valore predefinito è `false`. Impostare questa proprietà su `true` se si desidera utilizzare il metodo `sendBeacon` per inviare dati ad Adobe.

>[!IMPORTANT]
>
>La proprietà `documentUnloading` non è compatibile con la proprietà [`renderDecisions`](renderdecisions.md). Non impostare entrambe le proprietà contemporaneamente su `true`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
