---
title: Panoramica di Adobe Experience Platform Web SDK
description: Scopri come utilizzare Adobe Experience Platform Web SDK per integrare le funzionalità di Platform nel tuo sito web.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Panoramica di Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK è una libreria JavaScript lato client che consente ai clienti di Adobe Experience Cloud di interagire con i vari servizi nel [!DNL Experience Cloud] tramite Adobe Experience Platform Edge Network. Oltre alla libreria JavaScript, è disponibile [estensione tag](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) per informazioni sulle configurazioni dell’SDK web.

Per una guida dettagliata alla configurazione di Web SDK con i tag e all’invio di dati alle soluzioni, consulta [Tutorial sull’implementazione di Adobe Experience Cloud con Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Questo prodotto è in continua evoluzione e in continua crescita per supportare un numero sempre maggiore di casi d’uso. Per restare al passo con le ultime novità e scoprire cosa supporta attualmente, consulta la [pagina casi d’uso supportati](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] fa parte della raccolta che costituisce [!DNL Adobe Experience Edge]. [!DNL Experience Edge] è costituito dalle seguenti tecnologie:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** Un SDK JavaScript e un’estensione tag per semplificare notevolmente la distribuzione [!DNL Adobe] tecnologie.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Estensione dell’SDK per dispositivi mobili v5 per consentire ai clienti di utilizzare la nuova metodologia di implementazione
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Una rete globale distribuita di server che consente una nuova metodologia di distribuzione [!DNL Adobe] products

Il [!DNL Adobe Experience Edge] è un nuovo framework per la raccolta dati a bassa latenza, il pluggable computing e l’attivazione rapida dei dati su tutti i canali indirizzabili.

[!DNL Adobe Experience Edge] fornisce un singolo SDK consolidato per ogni canale (JavaScript, Mobile, Server-side), che invia i dati a un dominio Adobe comune (`adobedc.net`) e riceve un singolo payload per la distribuzione di dati ed esperienze.

Sul lato server, un gateway edge unificato e un framework di servizi di piattaforma comune semplificano il plug-in e l&#39;implementazione di nuove funzionalità in questo ambiente di elaborazione in tempo reale.  Tale architettura:

* Riduzione del time-to-value per il cliente
* Elimina la necessità di integrazioni &quot;point&quot;
* Migliora le prestazioni rispetto alle vecchie librerie
* Riduce i costi
* Aumenta la velocità dell&#39;innovazione
* Offre vantaggi competitivi duraturi ad Adobe ai clienti

Un unico sistema edge consolidato consente ai clienti di gestire le campagne pubblicitarie, di marketing o di personalizzazione su tutti i canali come un’esperienza integrata. Permette [!DNL Adobe] per offrire ai clienti servizi con un costo totale di proprietà inferiore.  Inoltre, contribuisce ad aumentare la velocità dell’innovazione dei prodotti rendendo collegabile il vantaggio in tempo reale e consentendo [!DNL Adobe] e ai suoi clienti di aggiungere più rapidamente nuove funzionalità e una logica definita dal cliente a tale sistema in tempo reale.

## Video introduttivo {#video}

Il seguente video offre una panoramica di Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Librerie sostituite da Web SDK {#sdks}

L’SDK per web non è solo un wrapper per le librerie esistenti. Si tratta di una libreria completamente nuova, creata appositamente per incorporare le funzionalità delle librerie esistenti. Il suo scopo è quello di risolvere le problematiche che richiedono l’attivazione dei tag nell’ordine giusto, l’incoerenza con le sfide del controllo delle versioni della libreria e una migliore gestione delle dipendenze. È un nuovo modo di implementare [!DNL Experience Cloud] ed è [open source](https://github.com/adobe/alloy).

L’SDK per web sostituisce i seguenti SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Oltre a una nuova libreria, esiste un nuovo endpoint che semplifica le richieste HTTP ad Adobi di soluzioni. In precedenza, Visitor.js inviava una chiamata di blocco al servizio ID visitatore, poi AT.js inviava una chiamata ad Adobe Target, DIL.js inviava una chiamata a Adobe Audience Manager e infine AppMeasurement.js inviava una chiamata ad Adobe Analytics. Questa nuova libreria ed endpoint possono recuperare un ID e recuperare un [!DNL Target] esperienza, invia dati a [!DNL Audience Manager], e trasmettere i dati a Adobe Experience Platform con una singola chiamata.

Il seguente video mostra Adobe Experience Platform [!DNL Web SDK] e ADOBE EXPERIENCE PLATFORM [!DNL Edge Network] in azione. L’esempio video utilizza una singola chiamata ad Adobe che invia i dati a [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], e [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migrazione dalle librerie esistenti a Web SDK {#migrating-to-web-sdk}

Per semplificare la migrazione da una delle [librerie esistenti](#sdks) In Web SDK, Adobe offre un percorso di aggiornamento semplificato, che consente di migrare ogni singola pagina del sito web a Web SDK, senza la necessità di migrare l’intero sito web contemporaneamente.

Questo significa che puoi utilizzare l’SDK per web in una pagina e lasciare le librerie esistenti nelle altre pagine, fino a quando non puoi migrarle anch’esse.

### Considerazioni sulla migrazione da at.js a Web SDK {#considerations}

Prima della migrazione delle pagine che utilizzano [!DNL at.js] in Web SDK, assicurati di abilitare le seguenti opzioni di configurazione di Web SDK. In questo modo il profilo del visitatore viene mantenuto durante la navigazione dalle pagine con [!DNL at.js] alle pagine tramite Web SDK.

* [&quot;idMigrationEnabled&quot;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&quot;targetMigrationEnabled&quot;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>Le seguenti funzioni di Target non sono supportate durante la migrazione da at.js a Web SDK:
> * [Offerte di reindirizzamento](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME e supporto tra più domini](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)

Dopo la migrazione da at.js a Web SDK, devi rimuovere `targetMigrationEnabled` dalla configurazione.



