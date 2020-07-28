---
title: Guida all'SDK Web per Adobi Experience Platform
seo-title: Guida all'SDK Web per Adobi Experience Platform
description: Scopri  Adobe Experience Platform SDK Web e come può essere utilizzato.
seo-description: consentire ai clienti dell'Adobe Experience Cloud di interagire con i vari servizi del Experience Cloud .
translation-type: tm+mt
source-git-commit: fc8b26e237821d5fa2d72fb38189894ed0b05271
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---


# Che cos&#39;è  Adobe Experience Platform Web SDK

 Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti dell&#39;Adobe Experience Cloud di interagire con i vari servizi nel [!DNL Experience Cloud] tramite l&#39;Adobe di  [!DNL Experience Platform Edge Network]. Oltre alla libreria JavaScript, è disponibile un&#39;estensione [](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) Launch per facilitare le configurazioni SDK Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce Experience Edge. Experience Edge è costituito da tre tecnologie:

* **[!DNL Adobe Experience Platform Web SDK]:**SDK JavaScript e[!DNL Launch]estensione per semplificare notevolmente[!DNL Adobe]le tecnologie di implementazione
* **SDK di Mobile Adobe Experience Platform:** Estensione all’SDK v5 per dispositivi mobili per consentire ai clienti di utilizzare la nuova metodologia di distribuzione
* **[!DNL Adobe Experience Platform Edge Network]:**Una rete distribuita globale di server che consente una nuova metodologia di implementazione[!DNL Adobe]dei prodotti

Il [!DNL Adobe Experience Edge] nuovo framework è per la raccolta di dati a bassa latenza, il computing collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un unico SDK consolidato per ogni canale (JavaScript, Mobile, lato server), che invia dati a un dominio  Adobe (`adobedc.net`) comune e riceve un singolo payload per la distribuzione di dati e esperienze.

Sul lato server, un gateway periferico unificato e un framework comune per i servizi di piattaforma facilitano il collegamento e l&#39;implementazione di nuove funzionalità in questo ambiente di elaborazione in tempo reale.  Tale architettura:

* Riduce il tempo cliente al valore
* Termina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduce i costi
* Aumenta la velocità dell&#39;innovazione
* Crea vantaggi competitivi duraturi per i clienti  Adobi

Un unico sistema Edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come un&#39;esperienza integrata.  Consente [!DNL Adobe] di fornire servizi con costi di proprietà totali inferiori per i clienti.  Consente inoltre di aumentare la velocità dell&#39;innovazione dei prodotti, rendendo il sistema collegabile in tempo reale e consentendo [!DNL Adobe] ai clienti di aggiungere più rapidamente nuove funzionalità e logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo

Il seguente video offre una panoramica dell’Adobe Experience Platform  [!DNL Web SDK] e [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK sostituiti da SDK Web  Adobe Experience Platform

 Adobe Experience Platform SDK Web sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Non si tratta solo di un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle sfide con i tag che devono essere attivati nell&#39;ordine giusto, incoerenze con le problematiche di controllo delle versioni della libreria e una migliore gestione delle dipendenze. Si tratta di un nuovo modo di implementare il sistema [!DNL Experience Cloud] ed è [open source](https://github.com/adobe/alloy).

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni di  Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata al Adobe Target , DIL.js aveva inviato una chiamata a  Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata a  Adobe Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un&#39; [!DNL Target] esperienza, inviare dati a [!DNL Audience Manager]e passare i dati al Adobe Experience Platform  in una singola chiamata.

Il seguente video illustra l’Adobe Experience Platform  [!DNL Web SDK] e [!DNL Edge Network] in azione. Nell&#39;esempio video viene utilizzata una singola chiamata a  Adobe che invia dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

## Introduzione

È consigliabile [consultare la guida](getting-started/quick-start-with-launch.md) introduttiva per un&#39;esercitazione rapida su come iniziare a utilizzare  Adobe Launch.

Questo prodotto è in continua evoluzione e continua crescita per supportare sempre più casi di utilizzo. Per essere al passo con le ultime novità, consulta la scheda [dei casi d’uso](https://github.com/adobe/alloy/projects/5)supportata. Teniamo aggiornati i casi di utilizzo attualmente supportati e quelli su cui stiamo lavorando per consentirvi di prendere le migliori decisioni possibili.

* **Casi di utilizzo non ancora supportati:** Si tratta di casi d’uso che sono nella nostra tabella di marcia e che saranno sostenuti in futuro.
* **Casi di utilizzo in corso:** Questi sono i casi d’uso che il team sta attualmente lavorando per completare per la release.
* **Casi di utilizzo supportati:** Questi sono i casi di utilizzo supportati e attualmente in uso.
* **Casi di utilizzo non supportati:** Questi sono i casi d&#39;uso che abbiamo deciso di non sostenere.
