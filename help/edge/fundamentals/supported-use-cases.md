---
title: Casi d’uso supportati con Adobe Experience Platform Web SDK
description: Scopri quali casi d’uso sono supportati con Adobe Experience Platform Web SDK.
keywords: sdk web;casi di utilizzo
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 14%

---


# Casi d’uso supportati

In questa pagina sono elencati i casi d’uso supportati per l’SDK per web, con collegamenti a informazioni aggiuntive.

## Generale

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| SDK singolo semplificato |  |
| Rete globale di raccolta dati |  |
| Consenso a grana grossa |  |
| Stringhe di consenso IAB 2.0 | [Supporto IAB TCF 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/overview.html?lang=en#consent) |
| Raccogli il consenso a grana fine | [Integrazione dell’SDK web con il consenso di Adobe 2.0](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/sdk.html#prerequisites) |
| Supporto ECID | Per informazioni sul recupero dell&#39;ECID, consulta la nostra documentazione [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) e [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Raccogliere più entità |  |
| Supporto di Device Graph (pubblico/privato) | [Documentazione](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Invia dati a più organizzazioni sulla pagina | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/interacting-with-multiple-properties.html?lang=en#fundamentals) |
| Report dettagliati degli errori e registri |  |
| Richieste di traccia lato client e lato server |  |
| Estensione Adobe Experience Platform Launch | [Documenti di estensione dell’SDK per web](../../tags/extensions/web/sdk/overview.md) |
| Strumenti di debug disponibili | [Estensione Debugger ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) e  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Inviare eventi di esperienza |  |
| Offer Decisioning | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=en#personalization) |
| Se il set di dati è abilitato per il profilo, la capacità di inviare dati a Profilo dati cliente in tempo reale in tempo reale |  |
| Inviare dati al Customer Journey Analytics in tempo reale |  |
| Scrivere il consenso al profilo | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/sdk.html?lang=en) |
| Inoltrare i dati lato server in tempo reale a terze parti | [Documentazione](../../tags/ui/event-forwarding/overview.md) |
| Supporto per lo spazio dei nomi identità |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Analytics for Target (A4T) |  |
| Nessuna latenza di Analytics for Target (A4T) |  |
| Assegnazione di tag a più suite |  |
| Filtro bot |  |
| Prop, eVar ed eventi |  |
| Supporto di ListVar per Adobe Analytics |  |
| Versione del sistema operativo e del browser |  |
| Variabili predefinite | [Variabili mappate automaticamente](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en#data-collection) |
| Regole VISTA/regole di elaborazione |  |
| Supporto degli attributi dei visitatori |  |
| Supporto per i collegamenti di uscita |  |
| Collegamenti personalizzati/collegamenti per download |  |
| Tracciamento dello stato e delle azioni |  |
| Serializzazione degli eventi per eventi standard |  |
| Variabile &quot;products&quot;  | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Tutti i tipi di attività |  |
| Supporto del Compositore esperienza visivo nativo e SPA | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=en#personalization) |
| Compositore basato su moduli |  |
| Supporto per mbox globale | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) |
| Mbox personalizzate | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#manually-rendering-content) |
| Analytics for Target (A4T) |  |
| Supporto ambientale |  |
| Supporto per Workspace |  |
| Collegamenti QA in Adobe Target |  |
| Target basato su geo/dispositivo in Adobe Target |  |
| Supporto degli attributi dei visitatori |  |
| Script di profilo |  |
| XDM diventa parametri mbox |  |
| Offerte di reindirizzamento supportate con reporting A4T | [Documentazione](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Aggiornamento del profilo di Target | [Documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=en#single-profile-update) |
| Raccomandazioni |  |
| ID di terze parti di mBox |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Audience Analytics |  |
| Condivisione dei segmenti in Adobe Analytics |  |
| Supporto degli attributi dei visitatori |  |
| Sincronizzazioni partner |  |
| Destinazioni URL |  |
| Destinazioni cookie |  |
| Supporto ambientale |  |
| Sincronizzazione dei namespace Adobe Experience Platform con le origini dati Audience Manager |  |
| ID autenticati o noti |  |

{style=&quot;table-layout:auto&quot;}
