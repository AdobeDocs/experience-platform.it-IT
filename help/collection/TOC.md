---
audience: user
solution: Data Collection
user-guide-title: Raccolta dati
breadcrumb-title: Raccolta dati
user-guide-description: Scopri come inviare dati a Adobe Experience Platform.
feature: Data Collection
role: Developer
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 30%

---


# Raccolta dati {#collection}

+ [Panoramica](home.md)
+ [Autorizzazioni](permissions.md)
+ BrightScript {#brightscript}
   + [Panoramica di BrightScript](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Panoramica di JavaScript](js/js-overview.md)
   + [Note sulla versione](js/release-notes.md)
   + Installazione {#install}
      + [Panoramica sull’installazione](js/install/overview.md)
      + [Libreria](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Build personalizzata](js/install/create-custom-build.md)
   + Comandi {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [Panoramica](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [contesto](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [prehidingStyle](js/commands/configure/prehidingstyle.md)
         + [pushNotifications](js/commands/configure/pushnotifications.md)
         + [streamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Panoramica](js/commands/sendevent/overview.md)
         + [dati](js/commands/sendevent/data.md)
         + [documentUnloading](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [personalizzazione](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [xdm](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Risposte ai comandi](js/commands/command-responses.md)
   + [Hook di monitoraggio](js/monitoring-hooks.md)
   + [Domande frequenti](js/faq.md)
+ Tag {#tags}
   + [Panoramica](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [azienda](tags/company.md)
   + [_contenitore](tags/container.md)
   + [cookie](tags/cookie.md)
   + [environment](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [_monitoraggi](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ Casi d’uso {#use-cases}
   + [Panoramica](use-cases/overview.md)
   + [Hint client](use-cases/client-hints.md)
   + [Stato client](use-cases/client-state.md)
   + [Raccogliere dati commerce](use-cases/collect-commerce-data.md)
   + [Configurare un CSP](use-cases/configuring-a-csp.md)
   + [Debug](use-cases/debugging.md)
   + [Deduplicazione degli eventi](use-cases/event-duplication.md)
   + Identità {#identity}
      + [Panoramica](use-cases/identity/id-overview.md)
      + [ID dispositivo di prime parti](use-cases/identity/first-party-device-ids.md)
      + [Condivisione ID](use-cases/identity/id-sharing.md)
   + [Più istanze SDK](use-cases/multiple-instances.md)
   + Personalizzazione {#personalization}
      + [Panoramica](use-cases/personalization/pers-overview.md)
      + [Visualizza eventi](use-cases/personalization/display-events.md)
      + [Gestisci visualizzazione momentanea di altri contenuti](use-cases/personalization/manage-flicker.md)
      + [Rendering di contenuti personalizzati](use-cases/personalization/rendering-personalization-content.md)
      + [Eventi pagina superiore e inferiore](use-cases/personalization/top-bottom-page-events.md)
