---
title: Note sulla versione di Adobe Experience Platform Web SDK
seo-title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione di Adobe Experience Platform Web SDK.
seo-description: Note sulla versione di Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Note sulla versione

## Versione 2.1.0

* Rimuovere il `syncIdentity` comando e supportare il passaggio di tali ID nel `sendEvent` comando.
* Supporto di IAB 2.0 Consent Standard.
* Supporto per il passaggio di ID aggiuntivi nel `setConsent` comando.
* Supporto per la sostituzione del `datasetId` comando nel `sendEvent` .
* Monitor di supporto ([Per saperne di più](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Passa `environment: browser` i dati contestuali dei dettagli di implementazione.
