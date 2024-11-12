---
title: Panoramica di Adobe Experience Platform Web Software Development Kit (SDK)
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel tuo sito web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti Adobe Experience Cloud di interagire con i propri servizi tramite l’Edge Network Adobe Experience Platform.

Puoi implementare Web SDK in due modi:

* Estensione tag [Web SDK](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Per ulteriori informazioni, consulta l&#39;esercitazione su come [implementare Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it).
* Implementazione manuale tramite la [libreria Web SDK JavaScript](install/library.md).

Questa guida include istruzioni per interagire con le soluzioni Experience Cloud utilizzando sia la libreria JavaScript dell’SDK Web che l’estensione tag.

## Edge Network Experience Platform {#edge-network}



L’SDK per web di Experience Platform fa parte dell’Edge Network di Adobe Experience Platform, che include:

* **[Experience Platform Web SDK](#overview)**: libreria JavaScript ed estensione tag per semplificare la distribuzione della tecnologia Adobe.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: estensione dell&#39;SDK mobile v5 per la nuova metodologia di distribuzione.
* **[Edge Network API](../server-api/overview.md)**: API lato server per casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. Puoi utilizzarlo su server, dispositivi IoT, set-top box e altri dispositivi.

L&#39;Edge Network fornisce la raccolta dati a bassa latenza, il computing collegabile e l&#39;attivazione rapida dei dati su tutti i canali indirizzabili. Offre un unico SDK consolidato per canali web, mobili e lato server, inviando dati a un dominio Adobe comune (`adobedc.net`) e ricevendo un singolo payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework di servizi di piattaforma comune semplificano l’implementazione di nuove funzionalità, fornendo al contempo i seguenti vantaggi:

* Diminuzione del time-to-value del cliente;
* Eliminare la necessità di integrazioni &quot;puntuali&quot;;
* Migliorare le prestazioni rispetto alle vecchie librerie;
* Diminuzione dei costi operativi;
* Aumentare la velocità dell&#39;innovazione;
* Creazione di vantaggi competitivi duraturi per i clienti Adobe.

Un sistema Edge consolidato consente di gestire campagne pubblicitarie, di marketing e di personalizzazione su tutti i canali. Riduce il costo totale di proprietà e supporta vari tipi di dati, consentendo di mappare il modello dati per l’utilizzo con più prodotti di Experience Cloud.

## Panoramica video {#video}

Guarda il video seguente per una panoramica del Adobe Experience Platform [!DNL Web SDK] e del [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Librerie sostituite da Web SDK {#sdks}

L’SDK per web è una nuova libreria open source creata da zero per integrare le funzionalità delle librerie esistenti. Risolve i problemi relativi all&#39;ordine di attivazione dei tag, alle incoerenze di versione e alla gestione delle dipendenze, offrendo un nuovo metodo [open source](https://github.com/adobe/alloy) per implementare [!DNL Experience Cloud].

L’SDK per web sostituisce:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Inoltre, introduce un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. In precedenza erano necessarie più chiamate per `Visitor.js`, `AT.js`, `DIL.js` e `AppMeasurement.js`. Ora una singola chiamata può recuperare un ID, recuperare un&#39;esperienza [!DNL Target], inviare dati a [!DNL Audience Manager] e passare dati a Adobe Experience Platform.

Guarda il video seguente per vedere Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network] in azione, utilizzando una singola chiamata per inviare dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrazione dalle librerie esistenti a Web SDK {#migrating-to-web-sdk}

Adobe offre un percorso di aggiornamento semplificato per semplificare la migrazione da una qualsiasi delle [librerie esistenti](#sdks) a Web SDK. Puoi eseguire la migrazione di ogni pagina del sito Web singolarmente, senza dover eseguire la migrazione dell’intero sito contemporaneamente. Puoi utilizzare l’SDK per web su alcune pagine, mentre le librerie esistenti rimangono su altre, consentendo una transizione graduale.

### Considerazioni sulla migrazione di `AT.js` a Web SDK {#considerations}

Prima di eseguire la migrazione delle pagine utilizzando `AT.js` a Web SDK, abilita le seguenti opzioni di configurazione di Web SDK per garantire che il profilo del visitatore venga mantenuto durante la navigazione tra le pagine.

* [&quot;idMigrationEnabled&quot;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Le seguenti funzionalità di Target non sono supportate durante la migrazione da `at.js` a Web SDK:
>
>* [Offerte di reindirizzamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME e supporto tra domini](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Dopo la migrazione da `AT.js` a Web SDK, rimuovi l&#39;opzione `targetMigrationEnabled` dalla configurazione.
