---
title: Panoramica dell’SDK per web Adobe Experience Platform
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel sito web.
keywords: SDK per web Adobe Experience Platform;SDK per web Platform;SDK per web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK per web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Panoramica di Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nel [!DNL Experience Cloud] tramite Adobe Experience Platform Edge Network. Oltre alla libreria JavaScript, esiste un [estensione tag](../tags/extensions/web/sdk/overview.md) per facilitare le configurazioni dell&#39;SDK web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce Experience Edge. Experience Edge è costituito da tre tecnologie:

* **[!DNL Adobe Experience Platform Web SDK]:** SDK JavaScript ed estensione tag per semplificare radicalmente la distribuzione  [!DNL Adobe] delle tecnologie
* **Adobe Experience Platform Mobile SDK:**  estensione dell’SDK per dispositivi mobili v5 per consentire ai clienti di utilizzare la nuova metodologia di distribuzione
* **[!DNL Adobe Experience Platform Edge Network]:** Una rete distribuita globale di server che consente una nuova metodologia di distribuzione  [!DNL Adobe] dei prodotti

Il [!DNL Adobe Experience Edge] è un nuovo framework per la raccolta di dati a bassa latenza, il calcolo collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un singolo SDK consolidato per ogni canale (JavaScript, Mobile, lato server), che invia dati a un dominio di Adobe comune (`adobedc.net`) e riceve un singolo payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework comune di servizi di piattaforma facilitano il plug-in e l&#39;implementazione di nuove funzionalità in questo ambiente informatico in tempo reale.  Tale architettura:

* Diminuisce il time-to-value del cliente
* Termina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduzione dei costi
* Aumenta la velocità dell&#39;innovazione
* Offre vantaggi competitivi duraturi per i clienti di Adobi

Un unico sistema Edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come esperienza integrata.  Permette a [!DNL Adobe] di fornire servizi con un costo totale di proprietà inferiore per i clienti.  Aiuta inoltre ad aumentare la velocità di innovazione del prodotto rendendo il dispositivo plug-in in tempo reale e consentendo a [!DNL Adobe] e ai suoi clienti di aggiungere più rapidamente nuove funzionalità e logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo

Il video seguente offre una panoramica di Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK sostituiti da Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Questo non è solo un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle sfide con i tag che devono attivarsi nell&#39;ordine giusto, incoerenza con le problematiche di gestione delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo per implementare il [!DNL Experience Cloud] ed è [open source](https://github.com/adobe/alloy).

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata ad Adobe Target, DIL.js aveva inviato una chiamata a Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un’esperienza [!DNL Target], inviare dati a [!DNL Audience Manager] e passare i dati a Adobe Experience Platform in una singola chiamata.

Il video seguente illustra Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] in azione. Nell&#39;esempio video viene utilizzata una singola chiamata all&#39;Adobe che invia i dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Questo prodotto è in continua evoluzione e in crescita per supportare sempre più casi d&#39;uso. Per essere sempre al passo con le ultime novità, consulta la pagina [casi d’uso supportati](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). In questa pagina sono elencati i casi d’uso attualmente supportati, con collegamenti a ulteriori informazioni quando disponibili.

* **Casi d’uso non ancora supportati:**  si tratta di casi d’uso che sono nella nostra roadmap e che devono essere supportati in futuro.
* **Casi d’uso in corso:**  questi sono i casi d’uso che il team sta attualmente cercando di completare per la versione.
* **Casi d’uso supportati:**  questi sono i casi d’uso supportati e funzionano attualmente.
* **Casi d’uso non supportati:** questi sono i casi d’uso che abbiamo deciso di non supportare.
