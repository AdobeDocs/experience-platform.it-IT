---
title: Panoramica di IAB Transparency & Consent Framework 2.0
seo-title: Supporto delle preferenze di consenso di Adobe Experience Platform Web SDK da Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Scopri come supportare le preferenze di consenso di IAB TCF 2.0 con  Experience Platform Web SDK
seo-description: Scopri come supportare le preferenze di consenso di IAB TCF 2.0 con  Experience Platform Web SDK
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 3f70e7fdd5888018f3814d1446042e96d2e53304
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 0%

---


# Panoramica di IAB Transparency &amp; Consent Framework 2.0

Adobe Experience Platform Web SDK supporta Interactive Advertising Bureau Transparency &amp; Consent Framework, versione 2.0 (IAB TCF 2.0). Questa guida illustra i requisiti per il supporto di IAB TCF 2.0 tramite Adobe Experience Platform Web SDK integrato con Real-time Customer Data Platform,  Audience Manager, Eventi esperienza,  Adobe Analytics ed Experience Edge.

Sono inoltre disponibili le seguenti guide per facilitare l&#39;apprendimento di come integrare IAB TCF 2.0 con e senza  Adobe Experience Platform Launch.

- [Con  Adobe Experience Platform Launch](./with-launch.md)
- [Senza  Adobe Experience Platform Launch](./without-launch.md)

## Introduzione

Per implementare l’SDK Web con IAB TCF 2.0, è necessario avere una conoscenza approfondita del modello dati esperienza (XDM) e degli eventi esperienza. Prima di iniziare, consulta il seguente documento:

- [Panoramica](../../../xdm/home.md)del sistema XDM (Experience Data Model): Standardizzazione e interoperabilità sono concetti chiave di Adobe Experience Platform. [!DNL Experience Data Model (XDM)], guidato da  Adobe, è uno sforzo per standardizzare i dati sull&#39;esperienza cliente e definire schemi per la gestione dell&#39;esperienza cliente.

## Integrazione con la piattaforma dati cliente in tempo reale

Basato su Adobe Experience Platform, la piattaforma dati cliente in tempo reale (Real-time CDP) consente di unire dati noti e anonimi provenienti da più origini aziendali. Questo consente di creare profili cliente che possono essere utilizzati per fornire esperienze cliente personalizzate in tempo reale su tutti i canali e i dispositivi. Per inviare i dati di consenso a CDP in tempo reale tramite l’SDK, è necessario quanto segue:

- Un dataset basato sulla [!DNL XDM Individual Profile] classe, abilitato per l&#39;uso in [!DNL Real-time Customer Profile], con il mixin privacy profilo.
- Configurazione edge configurata con CDP in tempo reale e set di dati del profilo sopra menzionati.

Fare riferimento all&#39;esercitazione sulla [creazione di set di dati per l&#39;acquisizione del consenso](../../../rtcdp/privacy/iab/dataset-preparation.md) TCF 2.0 per la creazione del set di dati richiesto.

Per istruzioni sulla creazione della configurazione dei bordi, fare riferimento alla panoramica [sulla conformità](../../../rtcdp/privacy/privacy-overview.md) IAB TCF 2.0.

## Integrazione  Audience Manager

Adobe Audience Manager (AAM) include il supporto per IAB TCF 2.0, che consente di valutare, onorare e inoltrare le scelte sulla privacy dei clienti ai partner a valle. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Per effettuare l’integrazione con  Audience Manager tramite Adobe Experience Platform Web SDK, accertatevi di disporre di una configurazione Edge impostata per l’inoltro ad Adobe Audience Manager.

## Eventi esperienza e integrazione  Adobe Analytics

Mentre il CDP in tempo reale e  Audienci Manager  pubblico tengono traccia delle preferenze di consenso correnti di un cliente, gli Eventi esperienza possono contenere le preferenze di consenso del cliente attive al momento della raccolta dell&#39;evento.

Per raccogliere le informazioni di consenso sugli eventi, è necessario quanto segue:

- Un set di dati basato sulla [!DNL XDM Experience Event] classe, con il mixin della [!DNL Experience Event] privacy.
- Configurazione edge configurata con il [!DNL XDM Experience Event] dataset sopra.

Per ulteriori informazioni su come convertire un evento esperienza XDM in un hit di Analytics, consulta la documentazione di panoramica [di](../../data-collection/adobe-analytics/analytics-overview.md) Analytics.

## Integrazione Adobe Experience Platform Web SDK

Le sezioni seguenti descrivono i punti di integrazione principali tra IAB TCF 2.0 e Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Anche senza la configurazione del CDP in tempo reale o del Audience Manager , è comunque possibile integrare IAB TCF 2.0 con l&#39;SDK Web. Le preferenze di consenso possono essere utilizzate per controllare la raccolta di Experience Events e per impostare un cookie di identità.

### Consenso predefinito

Il consenso predefinito viene utilizzato quando non esiste già una preferenza di consenso salvata per un cliente. Ciò significa che le opzioni di consenso predefinite possono controllare il comportamento di Adobe Experience Platform Web SDK e apportare modifiche in base all&#39;area geografica del cliente.

Ad esempio, se hai un cliente che non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR), il consenso predefinito potrebbe essere impostato su `in`, ma all&#39;interno della giurisdizione del GDPR, il consenso predefinito potrebbe essere impostato su `pending`. La piattaforma di gestione cloud (CMP) potrebbe rilevare la regione del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

Per ulteriori informazioni sul consenso predefinito, consulta la sezione relativa al consenso [predefinito](../../fundamentals/configuring-the-sdk.md#default-consent) nella documentazione di configurazione dell’SDK.

### Impostazione del consenso quando cambia

Adobe Experience Platform Web SDK dispone di un `setConsent` comando che comunica le preferenze di consenso del cliente a tutti i servizi del Adobe  utilizzando IAB TCF 2.0. Se vi state integrando con CDP in tempo reale, questo aggiorna il profilo del cliente. Se vi state integrando con  Audience Manager, questo aggiorna le informazioni del cliente. La chiamata imposta anche un cookie con una preferenza di consenso totale o nulla che controlla se gli eventi esperienza futuri possono essere inviati o meno. Si intende che tale azione venga chiamata ogni volta che il consenso cambia. Al caricamento delle pagine future, il cookie di consenso di Experience Edge verrà letto per determinare se gli Eventi esperienza possono essere inviati e se è possibile impostare un cookie di identità.

Come per  Audience Manager  integrazione IAB TCF 2.0, Experience Edge fornisce il consenso quando un cliente ha fornito il proprio consenso esplicito ai seguenti scopi:

- **Finalità 1:** Archiviare e/o accedere alle informazioni su un dispositivo
- **Finalità 10:** Sviluppare e migliorare i prodotti
- **Scopo speciale 1:** Protezione, prevenzione di frodi e debug. (Per i regolamenti IAB TCF, questo è sempre consentito)
- **Autorizzazione fornitore  Adobe:** Consenso per  Adobe (fornitore 565)

Per ulteriori informazioni sul `setConsent` comando, consulta la documentazione relativa al [supporto del consenso](../../consent/supporting-consent.md).

### Aggiunta di contenuto agli eventi esperienza

Adobe Experience Platform Web SDK dispone di un `sendEvent` comando che raccoglie un evento esperienza. Se effettui l’integrazione con Experience Events o  Adobe Analytics e desideri ottenere le preferenze di consenso per ogni Experience Event, devi aggiungere le informazioni di consenso a ogni `sendEvent` comando.

Per ulteriori informazioni sul `sendEvent` comando, consulta la documentazione relativa agli eventi [di](../../fundamentals/tracking-events.md)tracciamento.

## Passaggi successivi

Ora che si ha una conoscenza di base di IAB Transparency &amp; Consent Framework 2.0, fare riferimento a una delle guide sull&#39;utilizzo di IAB TCF 2.0 [con  Adobe Experience Platform Launch](./with-launch.md) o [senza  Adobe Experience Platform Launch](./without-launch.md).
