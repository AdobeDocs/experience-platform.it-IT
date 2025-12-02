---
title: Componenti di build personalizzati
description: Creare una build Web SDK personalizzata che disabilita le funzioni per ridurre le dimensioni della build.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Componenti di build personalizzati

La libreria SDK Web include più moduli per varie funzioni come personalizzazione, identità, tracciamento dei collegamenti e altro ancora. A seconda dei casi di utilizzo, potresti aver bisogno solo di funzionalità specifiche invece che dell’intera libreria. La disattivazione dei componenti di build consente di utilizzare solo i moduli necessari, riducendo le dimensioni della libreria e migliorando le prestazioni.

Quando disattivi un componente, non puoi più modificarne le impostazioni. Se utilizzi più istanze di Web SDK, i componenti di build selezionati si applicano a tutte le istanze.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Espandere il pannello a soffietto **[!UICONTROL Custom build components]** nella parte superiore.

>[!WARNING]
>
>Una modifica errata di queste impostazioni può causare risultati indesiderati, inclusa la perdita di dati. Esegui un test completo dell’implementazione in un ambiente di sviluppo prima di pubblicare queste modifiche nell’ambiente di produzione.

Adobe offre la possibilità di disattivare i seguenti componenti di build di Web SDK:

| Genera componente | Descrizione | Feature dipendenti |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Consente la raccolta di collegamenti automatica e il tracciamento di Activity Map. | |
| **[!UICONTROL Advertising]** | Abilita l’integrazione di Adobe Advertising con Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Supporta l&#39;integrazione con Adobe Audience Manager, ad esempio le sincronizzazioni ID. | |
| **[!UICONTROL Consent]** | Consente di utilizzare le funzioni di consenso. | Azione [[!UICONTROL Set consent]](../actions/set-consent.md) |
| **[!UICONTROL Event merge]** | Obsoleto. | [[!UICONTROL Event merge ID]](../data-element-types.md) elemento dati (obsoleto)<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) azione (obsoleto) |
| **[!UICONTROL Media Analytics bridge]** | Supporta l’integrazione con Media Analytics legacy. | Azione [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) |
| **[!UICONTROL Personalization]** | Supporta le integrazioni con Adobe Target e Adobe Journey Optimizer. | Azione [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) |
| **[!UICONTROL Push notifications]** | Abilita le notifiche push web per Adobe Journey Optimizer. | Azione [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) |
| **[!UICONTROL Rules engine]** | Abilita le decisioni sul dispositivo con Adobe Journey Optimizer. | Azione [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md)<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) evento |
| **[!UICONTROL Streaming media]** | Supporta l’integrazione con la raccolta di contenuti multimediali in streaming. | Azione [[!UICONTROL Send media event]](../actions/send-media-event.md) |
