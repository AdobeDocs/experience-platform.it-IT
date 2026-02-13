---
title: Impostazioni di configurazione Brand Concierge
description: Configura la persistenza della sessione e i timeout del flusso per la chat di Brand Concierge.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# Impostazioni di configurazione Brand Concierge {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge per Web SDK è attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Impostazioni di configurazione quando si utilizza Brand Concierge nella proprietà."

La sezione **[!UICONTROL Brand Concierge]** consente di controllare il comportamento delle sessioni di chat di Brand Concierge nell&#39;estensione tag Web SDK.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Brand Concierge]**.

Sono disponibili le seguenti opzioni:

## [!UICONTROL Sticky conversation session]

Casella di controllo che consente di salvare in modo permanente le sessioni Brand Concierge in più pagine utilizzando un cookie di sessione. Questa opzione è disabilitata per impostazione predefinita. Per istruzioni sull&#39;impostazione di questo valore, consulta [`conversation`](/help/collection/js/commands/configure/conversation.md) nella documentazione della libreria JavaScript.

## [!UICONTROL Stream timeout (seconds)]

Tempo massimo, in secondi, di attesa dei blocchi del flusso di conversazione prima che venga attivato un errore di timeout. Il valore predefinito è `10` secondi.
