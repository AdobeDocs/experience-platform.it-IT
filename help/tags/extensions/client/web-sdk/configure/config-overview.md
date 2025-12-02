---
title: Panoramica delle impostazioni di configurazione
description: Scopri le opzioni disponibili durante la configurazione dell’estensione tag Web SDK.
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Panoramica delle impostazioni di configurazione

L&#39;estensione tag Adobe Experience Platform Web SDK offre diverse opzioni personalizzabili. Queste impostazioni di configurazione equivalgono all&#39;utilizzo del comando [`configure`](/help/collection/js/commands/configure/overview.md) nella libreria JavaScript.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].

## Componenti di build personalizzati

Se l&#39;ottimizzazione della dimensione di build è una priorità per la tua organizzazione, puoi disabilitare alcune funzioni che non utilizzi per ridurre la dimensione di build dell&#39;estensione. Per ulteriori informazioni, vedere [Componenti di compilazione personalizzati](custom-build-components.md).

## Istanze di SDK

La maggior parte delle implementazioni in genere richiede una singola istanza di SDK. Tuttavia, se l&#39;organizzazione richiede più istanze di tracciamento di Web SDK, è possibile utilizzare il pulsante **[!UICONTROL Add instance]**. Durante la configurazione di ogni istanza di tag Web SDK sono disponibili le seguenti sezioni generali:

* [**[!UICONTROL SDK instance]**](general.md): impostazioni generali per l&#39;istanza. Tutti i campi di questa sezione sono obbligatori.
* [**[!UICONTROL Datastreams]**](datastreams.md): la posizione in cui desideri spostare i dati per ogni ambiente di tag.
* [**[!UICONTROL Consent]**](consent.md): impostazioni di consenso predefinite per l&#39;estensione.
* [**[!UICONTROL Identity]**](identity.md): impostazioni di migrazione di cookie e visitatori.
* [**[!UICONTROL Personalization]**](personalization.md): personalizza l&#39;esperienza del visitatore a livello individuale.
* [**[!UICONTROL Data collection]**](data-collection.md): includere o omettere gli elementi raccolti automaticamente.
* [**[!UICONTROL Streaming media]**](streaming-media.md): impostazioni specifiche per la raccolta di file multimediali in streaming.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): modificare le impostazioni di configurazione quando vengono soddisfatte determinate condizioni.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): specificare il percorso di base per Edge Network.
