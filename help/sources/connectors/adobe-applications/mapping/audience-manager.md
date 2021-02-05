---
keywords: ' Experience Platform;home;argomenti più comuni; mappatura Audience Manager;mappatura del gestore di audience'
solution: Experience Platform
title: Mapping dei campi per il connettore di origine Adobe Audience Manager
topic: overview
description: Scoprite come mappare i dati Adobe Audience Manager (in tempo reale, caricati e profili) ai campi XDM (Experience Data Model) corrispondenti per il connettore di origine del Audience Manager .
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


#  mapping dei campi Audience Manager

Le tabelle riportate di seguito contengono le mappature tra i campi nei dati Adobe Audience Manager (Tempo reale, Dati caricati e Dati profilo) e i campi XDM corrispondenti.

Per ulteriori informazioni su ciascun campo XDM, vedere il [dizionario dei campi XDM](../../../../xdm/schema/field-dictionary.md).

## Dati in tempo reale

Tipo: Dati in tempo reale

| Campo dati RealTime | Campo XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *Solo per spazi dei nomi presenti in endUserIds e solo per il primo valore.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Solo per gli spazi dei nomi presenti in endUserIds e solo per il primo valore.* |
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
