---
title: Invio di dati ad Adobe Audience Manager
seo-title: Invio di dati ad Adobe Audience Manager con Adobe Experience Platform Web SDK
description: Scopri come inviare dati ad Adobe Audience Manager con l’SDK Web della piattaforma Experience
seo-description: Scopri come inviare dati ad Adobe Audience Manager con l’SDK Web della piattaforma Experience
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager su Experience Platform Edge Networking

L’SDK Web per Adobe Experience Platform è integrato con Adobe Audience Manager e supporta l’invio e la ricezione di dati da Audience Manager, cookie e destinazioni URL e sincronizzazione ID.

## Abilitazione di Audience Manager

Per abilitare Audience Manager dovrete effettuare le seguenti operazioni:

- Abilita Audience Manager nella configurazione [](../../fundamentals/edge-configuration.md)edge.
- Abilita o disabilita cookie e destinazioni URL.
- Specifica del contenitore di sincronizzazione ID per le sincronizzazioni di partner esterni (facoltativo)

## Identità di sincronizzazione

L’SDK Web di Adobe Experience Platform supporta la possibilità di dichiarare gli ID cliente e i loro stati di autenticazione tramite il comando [SyncIdentity](../../fundamentals/identity.md) .

Il metodo syncIdentity utilizza gli spazi dei nomi del servizio [identità](../../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità. Come cliente Audience Manager, tutte le tue origini dati esistenti che utilizzano il tipo di ID: Cross-Device avrà automaticamente uno spazio dei nomi identità corrispondente. Per trovare lo spazio dei nomi identità corrispondente per l’origine dati Audience Manager, accedi ad Adobe Experience Platform e passa alla sezione Identità.

![Visualizzazione dell’interfaccia utente Spazi dei nomi](../../../assets/edge_configuration_identity.png)

Qui puoi cercare l’origine dati di Audience Manager in base al nome. Il metodo syncIdentity utilizza il simbolo di identità per specificare lo spazio dei nomi.

Qualsiasi nuova origine dati Audience Manager che utilizza il tipo di ID: Cross-Device genererà uno spazio dei nomi identità corrispondente. I cookie dei tipi di ID origine dati e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi spazio nomi identità creato in Adobe Experience Platform genererà un&#39;origine dati Audience Manager corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio nomi.
