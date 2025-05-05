---
title: Panoramica di Adobe Experience Platform Web Software Development Kit (SDK)
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Experience Platform nel tuo sito web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i propri servizi tramite Adobe Experience Platform Edge Network.

È possibile implementare il Web SDK in due modi:

* L&#39;estensione tag [Web SDK](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Per ulteriori informazioni, vedere il tutorial su come [implementare Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it).
* Implementazione manuale tramite la [libreria JavaScript di Web SDK](install/library.md).

Questa guida include istruzioni per interagire con le soluzioni Experience Cloud utilizzando sia la libreria JavaScript di Web SDK che l’estensione tag.

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK fa parte di Adobe Experience Platform Edge Network, che include:

* **[Experience Platform Web SDK](#overview)**: libreria JavaScript ed estensione tag per semplificare la distribuzione della tecnologia Adobe.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**: estensione del SDK mobile v5 per la nuova metodologia di distribuzione.
* **[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/)**: API lato server per casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. Puoi utilizzarlo su server, dispositivi IoT, set-top box e altri dispositivi.

Edge Network fornisce la raccolta dati a bassa latenza, il computing collegabile e l’attivazione rapida dei dati su tutti i canali indirizzabili. Offre un unico SDK consolidato per canali web, mobili e lato server, inviando dati a un dominio Adobe comune (`adobedc.net`) e ricevendo un unico payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework di servizi di piattaforma comune semplificano l’implementazione di nuove funzionalità, fornendo al contempo i seguenti vantaggi:

* Diminuzione del time-to-value del cliente;
* Eliminare la necessità di integrazioni &quot;puntuali&quot;;
* Migliorare le prestazioni rispetto alle vecchie librerie;
* Diminuzione dei costi operativi;
* Aumentare la velocità dell&#39;innovazione;
* Creazione di vantaggi competitivi duraturi per i clienti Adobe.

Un sistema Edge consolidato consente di gestire campagne pubblicitarie, di marketing e di personalizzazione su tutti i canali. Riduce il costo totale di proprietà e supporta vari tipi di dati, consentendo di mappare il modello dati per l’utilizzo con più prodotti Experience Cloud.

## Panoramica video {#video}

Guarda il video seguente per una panoramica del Adobe Experience Platform [!DNL Web SDK] e del [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/37267?quality=12&learn=on&captions=ita)

## Librerie sostituite dal Web SDK {#sdks}

Il Web SDK è una nuova libreria open-source creata da zero per integrare le funzionalità delle librerie esistenti. Risolve i problemi relativi all&#39;ordine di attivazione dei tag, alle incoerenze di versione e alla gestione delle dipendenze, offrendo un nuovo metodo [open source](https://github.com/adobe/alloy) per implementare [!DNL Experience Cloud].

Il Web SDK sostituisce:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Inoltre, introduce un nuovo endpoint che semplifica le richieste HTTP alle soluzioni Adobe. In precedenza erano necessarie più chiamate per `Visitor.js`, `AT.js`, `DIL.js` e `AppMeasurement.js`. Ora una singola chiamata può recuperare un ID, recuperare un&#39;esperienza [!DNL Target], inviare dati a [!DNL Audience Manager] e passare dati a Adobe Experience Platform.

Guarda il video seguente per vedere Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network] in azione, utilizzando una singola chiamata per inviare dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager] e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/3413666?captions=ita)

## Migrazione da librerie esistenti a Web SDK {#migrating-to-web-sdk}

Adobe offre un percorso di aggiornamento semplificato per semplificare la migrazione da una qualsiasi delle [librerie esistenti](#sdks) a Web SDK. Puoi eseguire la migrazione di ogni pagina del sito Web singolarmente, senza dover eseguire la migrazione dell’intero sito contemporaneamente. È possibile utilizzare il Web SDK su alcune pagine, mentre le librerie esistenti rimangono su altre, consentendo una transizione graduale.

### Considerazioni sulla migrazione di `AT.js` a Web SDK {#considerations}

Prima di eseguire la migrazione delle pagine che utilizzano `AT.js` a Web SDK, abilita le seguenti opzioni di configurazione di Web SDK per garantire che il profilo del visitatore venga mantenuto durante la navigazione tra le pagine.

* [&quot;idMigrationEnabled&quot;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>Le seguenti funzionalità di Target non sono supportate durante la migrazione da `at.js` a Web SDK:
>
>* [Offerte di reindirizzamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=it)
>* [CNAME e supporto tra domini](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html?lang=it)

Dopo la migrazione da `AT.js` al Web SDK, rimuovere l&#39;opzione `targetMigrationEnabled` dalla configurazione.
