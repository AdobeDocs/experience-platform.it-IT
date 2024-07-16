---
title: renderDecisions
description: Esegui il rendering di contenuti personalizzati idonei per il rendering automatico.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

La proprietà `renderDecisions` consente di forzare il Web SDK a eseguire il rendering di qualsiasi contenuto personalizzato idoneo per il rendering automatico.

## Eseguire il rendering di contenuti personalizzati tramite l’estensione tag Web SDK

Seleziona la casella di controllo **[!UICONTROL Esegui rendering delle decisioni di personalizzazione visiva]** all&#39;interno delle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Scorri verso il basso fino alla sezione [!UICONTROL Personalization], quindi seleziona la casella di controllo **[!UICONTROL Decisioni di personalizzazione visiva]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Eseguire il rendering di contenuti personalizzati utilizzando la libreria JavaScript dell’SDK per web

Impostare il valore booleano `renderDecisions` durante l&#39;esecuzione del comando `sendEvent`. Se omesso, il valore predefinito di questa proprietà sarà `false`. Impostare questa proprietà su `true` per eseguire automaticamente il rendering del contenuto personalizzato.

>[!IMPORTANT]
>
>La proprietà `renderDecisions` non è compatibile con la proprietà [`documentUnloading`](documentunloading.md). Non impostare entrambe le proprietà contemporaneamente su `true`.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
