---
keywords: Experience Platform;home;argomenti popolari;mappatura Audience Manager;mappatura di audience manager
solution: Experience Platform
title: Campi di mappatura per il connettore sorgente Adobe Audience Manager
description: Scopri come mappare i dati di Adobe Audience Manager (in tempo reale, onboarded e Profile) sui campi corrispondenti di Experience Data Model (XDM) per il connettore di origine Audience Manager.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---

# Audience Manager di mappature dei campi

Le tabelle seguenti contengono le mappature tra i campi dei dati Adobe Audience Manager (in tempo reale, onboarded e Profile data) e i campi XDM corrispondenti.

Vedi la [Dizionario dei campi XDM](../../../../xdm/schema/field-dictionary.md) per ulteriori informazioni su ciascun campo XDM.

## Dati in tempo reale

Tipo: Dati in tempo reale

| Campo dati in tempo reale | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo per i namespace presenti in endUserIds e solo per il primo valore.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo per i namespace presenti in endUserIds e solo per il primo valore.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → tipo</li><li>produttore →</li><li>marketingName → modello</li><li>modelNumber → modello</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → città</li><li>d_postal → postalCode</li><li>d_lat → latitudine</li><li>d_longitudine → longitudine</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome os </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Dati profilo

Tipo: Profilo XDM

| Campo profilo | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
