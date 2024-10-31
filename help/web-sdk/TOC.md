---
solution: Data Collection
audience: user
user-guide-title: Guida di Adobe Experience Platform Web SDK
breadcrumb-title: Guida di SDK Web
user-guide-description: Interagisci con i servizi di Experience Cloud tramite la rete Edge.
feature: Web SDK
role: Developer
source-git-commit: 02ae1fce01895d83d9c68248397e5288613ffe58
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 23%

---


# Adobe Experience Platform Web SDK {#web-sdk}

* [Panoramica dell’SDK web](home.md)
* [Note sulla versione](release-notes.md)
* Installazione di Web SDK {#install}
   * [Panoramica](install/overview.md)
   * [Installare Web SDK utilizzando l’estensione tag](install/extension.md)
   * [Installare l’SDK web utilizzando la libreria JavaScript](install/library.md)
   * [Installare l’SDK per web utilizzando il pacchetto NPM](install/npm.md)
* Comandi {#commands}
   * configura {#configure}
      * [Panoramica](commands/configure/overview.md)
      * [autoTrackPropositionInteractionsEnabled](commands/configure/autotrackpropositioninteractionsenabled.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [contesto](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [streamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [prehidingStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent {#sendevent}
      * [Panoramica](commands/sendevent/overview.md)
      * [dati](commands/sendevent/data.md)
      * [documentUnloading](commands/sendevent/documentunloading.md)
      * [personalizzazione](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [tipo](commands/sendevent/type.md)
      * [xdm](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Configurare gli override dello stream di dati](commands/datastream-overrides.md)
   * [Risposte ai comandi](commands/command-responses.md)

* Identità {#identity}
   * [Panoramica](identity/overview.md)
   * [ID dispositivo di prime parti](identity/first-party-device-ids.md)
   * [Condivisione ID da dispositivo mobile a web e tra domini](identity/id-sharing.md)

* Personalizzazione {#personalization}
   * [Gestire gli eventi di visualizzazione](personalization/display-events.md)
   * [Rendering di contenuti personalizzati](personalization/rendering-personalization-content.md)
   * [Personalization tramite implementazione ibrida](personalization/hybrid-personalization.md)
   * [Gestisci visualizzazione momentanea di altri contenuti](personalization/manage-flicker.md)
   * [Hook di monitoraggio](monitoring-hooks.md)
   * Adobe Target {#adobe-target}
      * [Panoramica](personalization/adobe-target/target-overview.md)
      * [Implementazione di un&#39;applicazione a pagina singola](personalization/adobe-target/spa-implementation.md)
      * [Accesso ai token di risposta](personalization/adobe-target/accessing-response-tokens.md)
      * [Utilizzo dell’ID di terze parti mbox](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Confronto della libreria at.js con Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Registrazione di Analytics for Target (A4T) {#a4t}
         * [Panoramica](personalization/adobe-target/analytics-logging/overview.md)
         * [Registrazione lato client](personalization/adobe-target/analytics-logging/client-side.md)
         * [Registrazione lato server](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer decisioning {#offer-decisioning}
      * [Panoramica](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Panoramica](personalization/ajo/overview.md)
      * [Implementazione di un&#39;applicazione a pagina singola](personalization/ajo/web-spa-implementation.md)
      * [Configurare il supporto per la messaggistica Web in-app in Web SDK](personalization/web-in-app-messaging.md)

* Consenso {#consent}
   * IAB Transparency and Consent Framework 2.0 {#iab-tcf}
      * [Panoramica](consent/iab-tcf/overview.md)
      * [Integrare con i tag](consent/iab-tcf/with-tags.md)
      * [Integrare senza tag](consent/iab-tcf/without-tags.md)

* Casi d’uso {#use-cases}
   * [Panoramica](use-cases/overview.md)
   * [Inviare dati ad Adobe Analytics tramite Web SDK](use-cases/adobe-analytics.md)
   * [Hint client agente utente](use-cases/client-hints.md)
   * [Raccogliere dati commerce](use-cases/collect-commerce-data.md)
   * [Configurazione di un CSP](use-cases/configuring-a-csp.md)
   * [Metodi di debug](use-cases/debugging.md)
   * [Utilizzare più istanze di Web SDK](use-cases/multiple-instances.md)
   * [Configurare gli eventi di pagina superiore e inferiore](use-cases/top-bottom-page-events.md)

* [Domande frequenti](faq.md)
* [Risorse](resources.md)
