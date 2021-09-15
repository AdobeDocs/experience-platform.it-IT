---
title: Casi d’uso supportati con Adobe Experience Platform Web SDK
description: Scopri quali casi d’uso sono supportati con Adobe Experience Platform Web SDK.
keywords: sdk web;casi di utilizzo
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 18%

---

# Casi d’uso supportati

In questa pagina sono elencati i casi d’uso supportati per l’SDK per web, con collegamenti a informazioni aggiuntive.

## Generale

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| SDK singolo semplificato |  |
| Rete globale di raccolta dati |  |
| Consenso a grana grossa |  |
| Raccogli il consenso dei clienti in base a vari standard | <ul><li>[Supporto per Adobe Consent 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[Supporto IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Integrare l’SDK per inviare i segnali di consenso a Edge Network](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| Supporto ECID | Per informazioni sul recupero dell&#39;ECID, consulta la nostra documentazione [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) e [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Raccogliere più entità |  |
| Supporto di Device Graph (pubblico/privato) | [Documentazione](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Invia dati a più organizzazioni sulla pagina | [Documentazione](./interacting-with-multiple-properties.md) |
| Report dettagliati degli errori e registri |  |
| Richieste di traccia lato client e lato server |  |
| estensione tag | [Documenti di estensione dell’SDK per web](../../tags/extensions/web/sdk/overview.md) |
| Strumenti di debug disponibili | [Estensione Debugger ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) e  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Inviare eventi di esperienza |  |
| Offer Decisioning | [Documentazione](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Se il set di dati è abilitato per il profilo, la capacità di inviare dati a Profilo dati cliente in tempo reale in tempo reale |  |
| Inviare dati al Customer Journey Analytics in tempo reale |  |
| Scrivere il consenso al profilo | [Documentazione](../../landing/governance-privacy-security/consent/sdk.md) |
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
| Variabili predefinite | [Variabili mappate automaticamente](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| Regole VISTA/regole di elaborazione |  |
| Supporto degli attributi dei visitatori |  |
| Supporto per i collegamenti di uscita |  |
| Collegamenti personalizzati/collegamenti per download |  |
| Tracciamento dello stato e delle azioni |  |
| Serializzazione degli eventi per eventi standard |  |
| Variabile &quot;products&quot;  | [Documentazione](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Caso d’uso | Ulteriori informazioni |
| --- | --- |
| Tutti i tipi di attività |  |
| Supporto del Compositore esperienza visivo nativo e SPA | [Documentazione](../personalization/adobe-target/spa-implementation.md) |
| Compositore basato su moduli |  |
| Supporto per mbox globale | [Documentazione](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Mbox personalizzate | [Documentazione](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analytics for Target (A4T) |  |
| Supporto ambientale |  |
| Supporto per Workspace |  |
| Collegamenti QA in Adobe Target |  |
| Target basato su geo/dispositivo in Adobe Target |  |
| Supporto degli attributi dei visitatori |  |
| Script di profilo |  |
| XDM diventa parametri mbox |  |
| Offerte di reindirizzamento supportate con reporting A4T | [Documentazione](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Aggiornamento del profilo di Target | [Documentazione](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Raccomandazioni |  |
| ID di terze parti di mBox |  |
| Token di risposta | [Documentazione](../personalization/adobe-target/accessing-response-tokens.md) |

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
