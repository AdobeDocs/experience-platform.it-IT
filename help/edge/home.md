---
title: Panoramica dell’SDK per web Adobe Experience Platform
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel sito web.
keywords: SDK per web Adobe Experience Platform;SDK per web Platform;SDK per web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;sdk web;SDK;SDK per web;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 92344ca9c2daf603d866c8a3cc4e92b72a382fb1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Panoramica di Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nel [!DNL Experience Cloud] tramite Adobe Experience Platform Edge Network. Oltre alla libreria JavaScript, è disponibile un [estensione tag](./extension/web-sdk-extension-configuration.md) per informazioni sulle configurazioni dell&#39;SDK per web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce Experience Edge. Experience Edge è costituito da tre tecnologie:

* **[!DNL Adobe Experience Platform Web SDK]:** SDK JavaScript ed estensione tag per semplificare notevolmente la distribuzione [!DNL Adobe] tecnologie
* **SDK di Adobe Experience Platform Mobile:** Estensione all’SDK per dispositivi mobili v5 per consentire ai clienti di utilizzare la nuova metodologia di distribuzione
* **[!DNL Adobe Experience Platform Edge Network]:** Una rete distribuita globale di server che consenta una nuova metodologia di distribuzione [!DNL Adobe] products

La [!DNL Adobe Experience Edge] è un nuovo framework per la raccolta di dati a bassa latenza, il calcolo collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un singolo SDK consolidato per ogni canale (JavaScript, Mobile, lato server), che invia dati a un dominio di Adobe comune (`adobedc.net`) e riceve un singolo payload per i dati e la distribuzione dell’esperienza.

Sul lato server, un gateway edge unificato e un framework comune di servizi di piattaforma facilitano il plug-in e l&#39;implementazione di nuove funzionalità in questo ambiente informatico in tempo reale.  Tale architettura:

* Diminuisce il time-to-value del cliente
* Termina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduzione dei costi
* Aumenta la velocità dell&#39;innovazione
* Offre vantaggi competitivi duraturi per i clienti di Adobi

Un unico sistema Edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come esperienza integrata.  Permette [!DNL Adobe] fornire servizi con un costo totale di proprietà inferiore per i clienti.  Aiuta inoltre ad aumentare la velocità dell&#39;innovazione del prodotto rendendo il bordo in tempo reale collegabile e permettendo [!DNL Adobe] e ai suoi clienti di aggiungere più rapidamente nuove funzionalità e logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo

Il video seguente offre una panoramica di Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK sostituiti da Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Questo non è solo un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle sfide con i tag che devono attivarsi nell&#39;ordine giusto, incoerenza con le problematiche di gestione delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo per implementare [!DNL Experience Cloud] e [open source](https://github.com/adobe/alloy).

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata ad Adobe Target, DIL.js aveva inviato una chiamata a Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata ad Adobe Analytics. Questa nuova libreria ed endpoint possono recuperare un ID, recuperare un [!DNL Target] esperienza, inviare dati a [!DNL Audience Manager], e passa i dati a Adobe Experience Platform in una singola chiamata.

Il video seguente illustra Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network] in azione. L’esempio video utilizza una singola chiamata all’Adobe che invia i dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Questo prodotto è in continua evoluzione e in crescita per supportare sempre più casi d&#39;uso. Per tenere il passo con le ultime novità, consulta [pagina dei casi d’uso supportati](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). In questa pagina sono elencati i casi d’uso attualmente supportati, con collegamenti a ulteriori informazioni quando disponibili.

* **Casi d’uso non ancora supportati:** Si tratta di casi d’uso che sono nella nostra tabella di marcia da supportare in futuro.
* **Casi d&#39;uso in corso:** Questi sono i casi d’uso che il team sta attualmente cercando di completare per la versione.
* **Casi d’uso supportati:** Questi sono i casi d’uso supportati e funzionano attualmente.
* **Casi di utilizzo non supportati:** Sono questi i casi d&#39;uso che abbiamo deciso di non sostenere.
