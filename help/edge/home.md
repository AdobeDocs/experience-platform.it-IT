---
title: Guida di Adobe Experience Platform Web SDK
seo-title: Guida di Adobe Experience Platform Web SDK
description: Scopri cos’è Adobe Experience Platform Web SDK e come può essere utilizzato.
seo-description: Scoprite come consentire ai clienti di Adobe Experience Cloud di interagire con i vari servizi del Experience Cloud .
keywords: SDK Web per Adobe Experience Platform;SDK per piattaforma Web;SDK per Web;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# Cos&#39;è Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi in [!DNL Experience Cloud] tramite Adobe Experience Platform Edge Network. Oltre alla libreria JavaScript, è disponibile un [estensione di Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) per facilitare le configurazioni SDK Web.

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce Experience Edge. Experience Edge è costituito da tre tecnologie:

* **[!DNL Adobe Experience Platform Web SDK]:** SDK JavaScript e  [!DNL Experience Platform Launch] estensione per semplificare notevolmente  [!DNL Adobe] le tecnologie di distribuzione
* **SDK di Adobe Experience Platform Mobile:** Estensione dell’SDK v5 per dispositivi mobili per consentire ai clienti di utilizzare la nuova metodologia di distribuzione
* **[!DNL Adobe Experience Platform Edge Network]:** Una rete distribuita globale di server che consente una nuova metodologia di implementazione  [!DNL Adobe] dei prodotti

Il [!DNL Adobe Experience Edge] è un nuovo framework per la raccolta di dati a bassa latenza, il computing collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un unico SDK consolidato per ogni canale (JavaScript, Mobile, lato server), che invia dati a un dominio  Adobe (`adobedc.net`) comune e riceve un singolo payload per la distribuzione di dati e esperienze.

Sul lato server, un gateway periferico unificato e un framework comune per i servizi di piattaforma facilitano il collegamento e l&#39;implementazione di nuove funzionalità in questo ambiente di elaborazione in tempo reale.  Tale architettura:

* Riduce il tempo cliente al valore
* Termina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduce i costi
* Aumenta la velocità dell&#39;innovazione
* Crea vantaggi competitivi duraturi per i clienti  Adobi

Un unico sistema Edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come un&#39;esperienza integrata.  Consente a [!DNL Adobe] di fornire servizi con costi di proprietà totali inferiori per i clienti.  Consente inoltre di aumentare la velocità dell&#39;innovazione dei prodotti, rendendo il sistema compatibile con i margini in tempo reale e consentendo a [!DNL Adobe] e ai suoi clienti di aggiungere più rapidamente nuove funzionalità e logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo

Il seguente video offre una panoramica dei prodotti Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK sostituiti da Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Non si tratta solo di un wrapper intorno alle librerie esistenti. È una riscrittura completa. Il suo scopo è quello di porre fine alle sfide con i tag che devono essere attivati nell&#39;ordine giusto, incoerenze con le problematiche di controllo delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo per implementare il [!DNL Experience Cloud] ed è [open source](https://github.com/adobe/alloy).

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP alle soluzioni di  Adobe. Prima, Visitor.js aveva inviato una chiamata di blocco al servizio ID visitatore, quindi AT.js aveva inviato una chiamata a  Adobe Target, DIL.js aveva inviato una chiamata ad Adobe Audience Manager e infine AppMeasurement.js aveva inviato una chiamata a  Adobe Analytics. Questa nuova libreria e questo endpoint possono recuperare un ID, recuperare un&#39;esperienza [!DNL Target], inviare dati a [!DNL Audience Manager] e passare i dati ad Adobe Experience Platform in una singola chiamata.

Il seguente video illustra l&#39;azione di Adobe Experience Platform [!DNL Web SDK] e Adobe Experience Platform [!DNL Edge Network]. Nell&#39;esempio video viene utilizzata una singola chiamata per  Adobe che invia dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Questo prodotto è in continua evoluzione e continua crescita per supportare sempre più casi di utilizzo. Per essere al passo con le ultime novità, consulta la nostra [scheda dei casi d&#39;uso supportata](https://github.com/adobe/alloy/projects/5). Teniamo aggiornati i casi di utilizzo attualmente supportati e quelli su cui stiamo lavorando per consentirvi di prendere le migliori decisioni possibili.

* **Casi d’uso non ancora supportati:** si tratta di casi d’uso che sono inclusi nella nostra tabella di marcia e che saranno supportati in futuro.
* **Casi d’uso in corso:** questi sono i casi d’uso a cui il team sta lavorando per completare il rilascio.
* **Casi di utilizzo supportati:** questi sono i casi di utilizzo supportati e attualmente in uso.
* **Casi di utilizzo non supportati:** questi sono i casi di utilizzo che abbiamo deciso di non supportare.
