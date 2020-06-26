---
title: Guida all'SDK Web per Adobi Experience Platform
seo-title: Guida all'SDK Web per Adobi Experience Platform
description: Scopri  Adobe Experience Platform SDK Web e come può essere utilizzato.
seo-description: consentire ai clienti di Adobe Experience Cloud di interagire con i vari servizi nell'Experience Cloud .
translation-type: tm+mt
source-git-commit: 3f52def8318f57cfc6534e15415d172e768a8614
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Che cos&#39;è  Adobe Experience Platform Web SDK

 Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi dell&#39;Experience Cloud  tramite  Adobe Experience Platform rete Edge.

## SDK sostituiti da SDK Web  Adobe Experience Platform

 Adobe Experience Platform SDK Web sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Non si tratta solo di un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle sfide con i tag che devono essere attivati nell&#39;ordine giusto, incoerenze con le problematiche di controllo delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo per implementare l&#39;Experience Cloud  ed è [open source](https://github.com/adobe/alloy).

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. In precedenza, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata al Adobe Target , DIL.js aveva inviato una chiamata a  Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe  Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un&#39; [!DNL Target] esperienza, inviare dati a  Audience Manager e trasmettere i dati al Adobe Experience Platform  in una singola chiamata.

## Introduzione

È consigliabile [consultare la guida](getting-started/quick-start-with-launch.md) introduttiva per un&#39;esercitazione rapida su come iniziare a utilizzare Adobe Launch.

Questo prodotto è in continua evoluzione e continua crescita per supportare sempre più casi di utilizzo. Per essere al passo con le ultime novità, consulta la scheda [dei casi d’uso](https://github.com/adobe/alloy/projects/5)supportata. Teniamo aggiornati i casi di utilizzo attualmente supportati e quelli su cui stiamo lavorando per consentirvi di prendere le migliori decisioni possibili.

* __Casi di utilizzo non ancora supportati__ - Si tratta di casi di utilizzo che sono nella nostra tabella di marcia per essere supportati in futuro.
* __Casi di utilizzo in corso__ : questi sono i casi di utilizzo per i quali il team sta attualmente lavorando per completare il rilascio.
* __Casi__ di utilizzo supportati: si tratta dei casi di utilizzo supportati e attualmente in uso.
* __Casi di utilizzo non supportati__ - Questi sono i casi di utilizzo che abbiamo deciso di non supportare.
