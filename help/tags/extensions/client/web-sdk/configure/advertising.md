---
title: Impostazioni di configurazione di Adobe Advertising
description: Abilita o disabilita la funzionalità della piattaforma lato domanda.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Impostazioni di configurazione di Adobe Advertising

>[!AVAILABILITY]
>
>Adobe Advertising per Web SDK è attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

La sezione **[!UICONTROL Adobe Advertising]** consente di abilitare o disabilitare la funzionalità di Demand-side Platform (DSP) se utilizzata nell&#39;implementazione. Devi impostare questo campo solo se l’implementazione utilizza un DSP.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Adobe Advertising]**.

Attualmente, è disponibile un’opzione.

## [!UICONTROL Adobe Advertising DSP]

Menu a discesa che abilita o disabilita la funzionalità DSP per Adobe Advertising.

* **[!UICONTROL Enabled]**: abilita il tracciamento view-through.
* **[!UICONTROL Disabled]**: disabilita il tracciamento view-through.

Quando questa opzione è attivata, sono disponibili le seguenti impostazioni:

* **[!UICONTROL Advertisers]**: gli inserzionisti per i quali abilitare il tracciamento view-through.
* **[!UICONTROL ID5 partner ID]**: facoltativo. ID del partner ID5 della tua organizzazione. Questa impostazione consente al Web SDK di raccogliere ID5 universali.
* **[!UICONTROL RampID JavaScript path]**: facoltativo. Percorso del codice JavaScript [!DNL LiveRamp RampID] della tua organizzazione (`ats.js`).  Questa impostazione consente al Web SDK di raccogliere [!DNL RampID] ID universali.
