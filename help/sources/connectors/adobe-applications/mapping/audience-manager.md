---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Campo di mappatura Audience Manager '
topic: overview
translation-type: tm+mt
source-git-commit: a1b09f3e88e489f1b0ec0c1fcb72a2a5a4356d87
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


#  campi di mappatura Audience Manager

Le tabelle riportate di seguito contengono le mappature tra i campi nei dati Adobe Audience Manager (Tempo reale, Dati caricati e Dati profilo) e i campi XDM corrispondenti.

Per ulteriori informazioni su ciascun campo XDM, vedere il dizionario [dei campi](../../../../xdm/schema/field-dictionary.md) XDM.

## Dati in tempo reale

Tipo: Dati in tempo reale

| Campo dati RealTime | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Solo per spazi dei nomi presenti in endUserIds e solo per il primo valore.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo per spazi di nomi presenti in endUserIds e solo per il primo valore.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>PrimaryHardwareType → type</li><li>produttore → produttore</li><li>marketingName →, modello</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → città</li><li>d_postal → postalCode</li><li>d_lat → latitudine</li><li>d_longitudine → longitudine</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nome os </li><li>d_os_version → os_version</li></ul> |

## Dati profilo

Tipo: Profilo XDM

| Campo profilo | Campo XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
