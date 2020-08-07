---
title: Note sulla versione di Adobe Experience Platform Web SDK
seo-title: Note sulla versione di Adobe Experience Platform Web SDK
description: Note sulla versione di Adobe Experience Platform Web SDK.
seo-description: Note sulla versione di Adobe Experience Platform Web SDK.
translation-type: tm+mt
source-git-commit: e9a49c20f30d06fa125185865b4963c8472fa5e5
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
