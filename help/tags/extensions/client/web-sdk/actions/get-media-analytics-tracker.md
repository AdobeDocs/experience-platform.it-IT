---
title: Ottieni tracciamento Media Analytics
description: Esporta l’API di contenuti multimediali precedenti in un oggetto finestra.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# Ottieni tracciamento Media Analytics

L&#39;azione **[!UICONTROL Get Media Analytics tracker]** viene utilizzata per ottenere l&#39;API legacy di Media Analytics. Quando si configura l’azione e viene fornito il nome di un oggetto, l’API legacy di Media Analytics viene esportata nell’oggetto finestra in questione. Questa azione è utile per passare da Media Analytics legacy a Streaming Media Analytics.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Get Media Analytics tracker]**.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione Ottieni tracciatore di Media Analytics.](../assets/get-media-analytics-tracker.png)

Questa azione contiene un singolo campo che puoi configurare:

* **[!UICONTROL Export the Media Legacy API to this window object]**: seleziona l&#39;oggetto desiderato in cui esportare l&#39;API Media Legacy. Se non viene specificato alcun valore, l&#39;azione esporta l&#39;API in `window.Media`.
