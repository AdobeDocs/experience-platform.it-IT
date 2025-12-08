---
title: Panoramica della libreria JavaScript di Web SDK
description: Invia dati a Adobe Experience Platform Edge Network tramite JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Panoramica della libreria JavaScript di Web SDK

**Adobe Experience Platform Web SDK** è una libreria JavaScript lato client che consente di inviare dati a Adobe Experience Platform Edge Network. Questa guida illustra il percorso di implementazione della libreria JavaScript di Web SDK (`alloy.js`), inclusi i concetti di base, l&#39;installazione, la configurazione e i comandi. Per informazioni sull&#39;estensione tag Web SDK nell&#39;interfaccia utente di Data Collection, vedere l&#39;estensione tag [Web SDK](/help/tags/extensions/client/web-sdk/overview.md).

Il SDK web invia i dati in modo indipendente dalla soluzione (XDM) all’Edge Network di Experience Platform, che quindi li mappa su formati e destinazioni specifici della soluzione e li invia in tempo reale.

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network fornisce la raccolta dati a bassa latenza, l’elaborazione collegabile e l’attivazione rapida dei dati su tutti i canali indirizzabili. Offre un unico SDK consolidato per canali web, mobili e lato server, inviando dati a un dominio Adobe comune (`adobedc.net`) e ricevendo un unico payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework di servizi di piattaforma comune semplificano l’implementazione di nuove funzionalità, fornendo al contempo i seguenti vantaggi:

* Diminuzione del time-to-value del cliente;
* Eliminare la necessità di integrazioni &quot;puntuali&quot;;
* Migliorare le prestazioni rispetto alle vecchie librerie;
* Diminuzione dei costi operativi;
* Aumentare la velocità dell&#39;innovazione;
* Creazione di vantaggi competitivi duraturi per i clienti Adobe.

Un sistema Edge consolidato consente di gestire campagne pubblicitarie, di marketing e di personalizzazione su tutti i canali. Riduce il costo totale di proprietà e supporta vari tipi di dati, consentendo di mappare il modello dati per l’utilizzo con più prodotti Experience Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/37267?captions=ita&quality=12&learn=on)

## Librerie sostituite dal Web SDK {#sdks}

Il Web SDK è una libreria open source creata da zero per integrare le funzionalità delle librerie esistenti. Risolve i problemi relativi all’ordine di attivazione dei tag, alle incoerenze di versione e alla gestione delle dipendenze, offrendo un modo per implementare molti prodotti Experience Cloud. Il Web SDK sostituisce la raccolta dati per i seguenti servizi:

* Servizio ID visitatore di Adobe Experience Platform (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Inoltre, introduce un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. In precedenza, erano necessarie più chiamate per ogni libreria di raccolta dati. Ora una singola chiamata può recuperare un ID, recuperare un&#39;esperienza [!DNL Target], inviare dati a [!DNL Audience Manager] e passare dati a Adobe Experience Platform.

## Migrazione da librerie esistenti a Web SDK {#migrating-to-web-sdk}

Adobe offre un percorso di aggiornamento semplificato per semplificare la migrazione da una qualsiasi delle librerie esistenti al Web SDK. Puoi eseguire la migrazione di ogni pagina del sito Web singolarmente, senza dover eseguire la migrazione dell’intero sito contemporaneamente. È possibile utilizzare il Web SDK su alcune pagine, mentre le librerie esistenti rimangono su altre, consentendo una transizione graduale.
