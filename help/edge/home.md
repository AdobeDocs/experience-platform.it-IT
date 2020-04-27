---
title: Guida all’SDK Web per Adobe Experience Platform
seo-title: Guida all’SDK Web per Adobe Experience Platform
description: Scopri cos’è Adobe Experience Platform Web SDK e come può essere utilizzato.
seo-description: consentire ai clienti di Adobe Experience Cloud di interagire con i vari servizi in Experience Cloud
translation-type: tm+mt
source-git-commit: 6ad09df6f6867ebe057d0043dea4bc97de2b66b3

---


# (Beta) Cos’è Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi di Experience Cloud tramite Adobe Experience Platform Edge Network.

## SDK sostituiti da Adobe Experience Platform Web SDK

L’SDK Web di Adobe Experience Platform sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Non si tratta solo di un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle problematiche relative ai tag attivati nell&#39;ordine corretto, alle incoerenze con i problemi di controllo delle versioni della libreria e a una migliore gestione delle dipendenze. È un nuovo modo per implementare Experience Cloud.

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata ad Adobe Target, DIL.js aveva inviato una chiamata ad Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un&#39;esperienza Target, inviare dati ad Audience Manager e passare i dati ad Adobe Experience Platform in una singola chiamata.