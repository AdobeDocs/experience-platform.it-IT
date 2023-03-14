---
keywords: Experience Platform;home;argomenti popolari;mappatura Audience Manager;mappatura audience manager
solution: Experience Platform
title: Campi di mappatura per il connettore di origine di Adobe Audience Manager
description: Scopri come mappare i dati di Adobe Audience Manager (dati in tempo reale, onboarded e profilo) sui campi Experience Data Model (XDM) corrispondenti per il connettore di origine dell’Audience Manager.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Audience Manager di mappature campi

Le tabelle seguenti contengono le mappature tra i campi nei dati di Adobe Audience Manager (dati in tempo reale, onboarded e profilo) e i relativi campi XDM corrispondenti.

Consulta la sezione [Dizionario campo XDM](../../../../xdm/schema/field-dictionary.md) per ulteriori informazioni su ciascun campo XDM.

## Dati in tempo reale

Tipo: dati in tempo reale

| Campo dati in tempo reale | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo per gli spazi dei nomi presenti in endUserIds e solo per il primo valore.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo per gli spazi dei nomi presenti in endUserIds e solo per il primo valore.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>tipo di → primaryHardwareType</li><li>produttore → produttore</li><li>modello di → marketingName</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → city</li><li>d_postalCode →</li><li>d_lat → latitudine</li><li>d_longitudine → longitudine</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome del sistema operativo </li><li>d_os_version → os_version</li></ul> |

{style="table-layout:auto"}

## Dati profilo

Tipo: profilo XDM

| Campo profilo | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style="table-layout:auto"}
