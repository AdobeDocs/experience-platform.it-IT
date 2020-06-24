---
title: Invio di dati a  Adobe Audience Manager
seo-title: Invio di dati a  Adobe Audience Manager con  Adobe Experience Platform Web SDK
description: Scopri come inviare dati a  Adobe Audience Manager con  Experience Platform Web SDK
seo-description: Scopri come inviare dati a  Adobe Audience Manager con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


#  Audience Manager su Experience Platform Edge Network 

L’SDK Web  Adobe Experience Platform è integrato con  Adobe Audience Manager e supporta l’invio e la ricezione di dati da  destinazioni Audience Manager, Cookie &amp; URL e la sincronizzazione ID.

## Abilitazione  Audience Manager

Per abilitare  Audience Manager dovrete effettuare le seguenti operazioni:

- Abilitate  Audience Manager nella configurazione [](../../fundamentals/edge-configuration.md)edge.
- Abilita o disabilita cookie e destinazioni URL.
- Specifica del contenitore di sincronizzazione ID per le sincronizzazioni di partner esterni (facoltativo)

## Identità di sincronizzazione

 Adobe Experience Platform Web SDK supporta la possibilità di dichiarare gli ID cliente e i loro stati di autenticazione tramite il comando [SyncIdentity](../../fundamentals/identity.md) .

Il metodo syncIdentity utilizza gli spazi dei nomi del servizio [identità](../../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità. Come cliente Audience Manager , tutte le tue Origini dati esistenti che utilizzano il Tipo ID: Cross-Device avrà automaticamente uno spazio dei nomi identità corrispondente. Per trovare lo spazio dei nomi identità corrispondente per l&#39;origine dati Audience Manager , accedere al Adobe Experience Platform  e passare alla sezione Identità.

![Visualizzazione dell’interfaccia utente Spazi dei nomi](../../../assets/edge_configuration_identity.png)

Qui puoi cercare la tua origine dati Audience Manager  per nome. Il metodo syncIdentity utilizza il simbolo di identità per specificare lo spazio dei nomi.

Qualsiasi nuova origine dati Audience Manager  che utilizza il tipo di ID: Cross-Device genererà uno spazio dei nomi identità corrispondente. I cookie dei tipi di ID origine dati e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi spazio nomi identità creato in  Adobe Experience Platform genererà un&#39;origine dati Audience Manager  corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio nomi.
