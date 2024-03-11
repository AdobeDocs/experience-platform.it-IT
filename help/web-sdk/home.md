---
title: Panoramica di Adobe Experience Platform Web Software Development Kit (SDK)
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel tuo sito web.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>Alla fine di aprile 2024, Adobe Experience Platform Web SDK rimuoverà il supporto per tutte le versioni di Internet Explorer.

Adobe Experience Platform Web Software Development Kit (SDK) è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i propri servizi tramite la rete Edge di Adobe Experience Platform.

Adobe offre due metodi per implementare Web SDK:

* Il [Estensione tag Web SDK](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Guarda il tutorial su come [implementare Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it) per ulteriori informazioni.
* Implementazione manuale tramite la libreria JavaScript dell’SDK web.

Questa guida utente include istruzioni sull’interazione con le soluzioni Experience Cloud tramite la libreria JavaScript di Web SDK e l’estensione tag, se applicabile.

## Experienci Platform Edge Network {#edge-network}

Experienci Platform Web SDK fa parte di una raccolta di strumenti che costituiscono la rete Edge di Adobe Experience Platform.

La rete Edge è costituita dai seguenti componenti:

* **[Experienci Platform Web SDK](#overview):** Una libreria JavaScript e un’estensione tag che consentono di semplificare la distribuzione di tecnologie Adobe.
* **[Experienci Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/):** Estensione dell’SDK per dispositivi mobili v5 che consente di utilizzare la nuova metodologia di distribuzione.
* **[API server di rete Edge](../server-api/overview.md):** API lato server che puoi utilizzare per vari casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. L’API server può essere utilizzata su server, dispositivi IoT, set-top box e vari altri dispositivi.

La rete Edge è un framework per la raccolta dati a bassa latenza, il pluggable computing e la rapida attivazione dei dati su tutti i canali indirizzabili. Fornisce un singolo SDK consolidato per ogni canale (web, mobile, lato server), che invia dati a un dominio Adobe comune (`adobedc.net`) e riceve un singolo payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework di servizi di piattaforma comune semplificano l&#39;implementazione di nuove funzionalità in questo ambiente di elaborazione in tempo reale. Tale architettura:

* Riduzione del time-to-value per il cliente
* Elimina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduce i costi
* Aumenta la velocità dell&#39;innovazione
* Offre vantaggi competitivi duraturi ad Adobe ai clienti

Un singolo sistema Edge consolidato consente di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come un’esperienza integrata. Consente inoltre ad Adobe di fornire servizi con un costo totale di proprietà inferiore per i clienti. Il sistema Edge è progettato per accogliere la maggior parte dei tipi di dati, consentendoti di mappare il tuo modello di dati in modo che possa essere acquisito da più prodotti Experience Cloud.

## Video introduttivo {#video}

Guarda il video seguente per una panoramica di Adobe Experience Platform [!DNL Web SDK] e [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Librerie sostituite da Web SDK {#sdks}

L’SDK per web non è solo un wrapper per le librerie esistenti. Si tratta di una nuova libreria, creata appositamente per incorporare le funzionalità delle librerie esistenti. Il suo scopo è quello di risolvere le problematiche che richiedono l’attivazione dei tag nell’ordine giusto, l’incoerenza con le sfide del controllo delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo di implementare [!DNL Experience Cloud] ed è [open source](https://github.com/adobe/alloy).

L’SDK per web sostituisce i seguenti SDK:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP ad Adobi di soluzioni. Prima di, `Visitor.js` ha inviato una chiamata di blocco al servizio ID visitatore, quindi `AT.js` ha inviato una chiamata ad Adobe Target, `DIL.js` ha inviato una chiamata a Adobe Audience Manager e infine `AppMeasurement.js` ha inviato una chiamata ad Adobe Analytics. Questa nuova libreria ed endpoint possono recuperare un ID e recuperare un [!DNL Target] esperienza, invia dati a [!DNL Audience Manager], e trasmettere i dati a Adobe Experience Platform con una singola chiamata.

Il seguente video mostra Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network] in azione. L’esempio video utilizza una singola chiamata ad Adobe che invia i dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrazione dalle librerie esistenti a Web SDK {#migrating-to-web-sdk}

Per semplificare la migrazione da una delle [librerie esistenti](#sdks) a Web SDK, Adobe offre un percorso di aggiornamento semplificato. Questo percorso consente di migrare ogni singola pagina del sito web a Web SDK senza la necessità di migrare l’intero sito web contemporaneamente. Puoi utilizzare l’SDK web in una determinata pagina mentre le librerie esistenti risiedono su altre pagine. Quando sei pronto, puoi eseguire anche la migrazione delle altre pagine.

### Migrazione di `AT.js` alle considerazioni sull’SDK per web {#considerations}

Prima della migrazione delle pagine che utilizzano `AT.js` in Web SDK, assicurati di abilitare le seguenti opzioni di configurazione di Web SDK. Queste opzioni garantiscono che il profilo del visitatore venga mantenuto durante la navigazione dalle pagine con `AT.js` alle pagine tramite Web SDK.

* [&quot;idMigrationEnabled&quot;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&quot;targetMigrationEnabled&quot;](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>Le seguenti funzioni di Target non sono supportate durante la migrazione da at.js a Web SDK:
>
>* [Offerte di reindirizzamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME e supporto tra più domini](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Dopo la migrazione da `AT.js` all’SDK per web, rimuovi il `targetMigrationEnabled` dalla configurazione.
