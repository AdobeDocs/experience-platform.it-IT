---
title: Guida all’SDK Web per Adobe Experience Platform
seo-title: Guida all’SDK Web per Adobe Experience Platform
description: Scopri cos’è Adobe Experience Platform Web SDK e come può essere utilizzato.
seo-description: consentire ai clienti di Adobe Experience Cloud di interagire con i vari servizi in Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Che cos’è Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi di Experience Cloud tramite Adobe Experience Platform Edge Network.

## SDK sostituiti da Adobe Experience Platform Web SDK

L’SDK Web di Adobe Experience Platform sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Non si tratta solo di un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle problematiche relative ai tag attivati nell&#39;ordine corretto, alle incoerenze con i problemi di controllo delle versioni della libreria e a una migliore gestione delle dipendenze. È un nuovo modo per implementare Experience Cloud ed è [open source](https://github.com/adobe/alloy)

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata ad Adobe Target, DIL.js aveva inviato una chiamata ad Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un&#39;esperienza Target, inviare dati ad Audience Manager e passare i dati ad Adobe Experience Platform in una singola chiamata.

## Introduzione

Per un’esercitazione rapida su come iniziare a usare il lancio, ti consigliamo di [consultare la nostra guida](getting-started/quick-start-with-launch.md) introduttiva.

Questo prodotto è in continua evoluzione e continua crescita per supportare sempre più casi di utilizzo. Per essere sempre al passo con gli ultimi aggiornamenti, consulta la nostra bacheca [](https://github.com/adobe/alloy/projects/5)supportata. Teniamo aggiornati i casi di utilizzo attualmente supportati e quelli su cui stiamo lavorando per consentirvi di prendere le migliori decisioni possibili.

* __Casi di utilizzo non ancora supportati__ - sono casi di utilizzo che sono nella nostra tabella di marcia da fare in futuro.
* __Casi di utilizzo in corso__ : questi sono i casi di utilizzo per i quali il team sta attualmente lavorando per completare il rilascio.
* __Casi__ di utilizzo supportati: si tratta dei casi di utilizzo supportati e attualmente in uso.
* __Casi di utilizzo non supportati__ - Questi sono i casi di utilizzo che abbiamo deciso di non supportare.
