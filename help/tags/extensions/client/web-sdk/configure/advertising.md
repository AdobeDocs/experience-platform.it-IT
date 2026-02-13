---
title: Impostazioni di configurazione di Adobe Advertising
description: Abilita o disabilita la funzionalità della piattaforma lato domanda.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Impostazioni di configurazione di Adobe Advertising {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising per Web SDK è attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Configura le impostazioni per le integrazioni Adobe Advertising. Tieni presente che non è necessaria alcuna configurazione pubblicitaria per abilitare la misurazione click-through. I client Search, Social e Commerce non richiedono ulteriori azioni; tuttavia, gli utenti di Demand-side Platform (DSP) devono configurare gli inserzionisti in questa sezione per misurare le conversioni view-through."

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
