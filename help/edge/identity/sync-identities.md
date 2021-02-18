---
title: Sincronizzazione delle identità tra  Audience Manager e Adobe Experience Platform mediante l'SDK Web della piattaforma
description: Scoprite come sincronizzare le identità tra  Audience Manager e Adobe Experience Platform utilizzando l'SDK Web per la piattaforma
seo-description: Scopri come sincronizzare le identità con Adobe Audience Manager con  SDK Web per Experienci Platform
keywords: audience manager;aam;identities;sync identities;namespace;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronizzazione delle identità tra  Audience Manager e  Experience Platform

Adobe Experience Platform Web SDK supporta la possibilità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite il comando [sendEvent](./overview.md#syncing-identities).

Scegliere gli spazi dei nomi da [Spazi dei nomi dei servizi di identità](../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità, utilizzando i valori nella colonna Simbolo di identità:

![Visualizzazione dell’interfaccia utente Spazi dei nomi](../../assets/edge_namespaceUI_identity-symbol.png)

Come cliente di  Audience Manager, tutte le tue Origini dati esistenti che utilizzano il tipo di ID: Cross-Device dispone automaticamente di uno spazio dei nomi identità corrispondente. Per trovare lo spazio dei nomi identità corrispondente per l&#39;origine dati  Audience Manager, accedere ad Adobe Experience Platform e passare alla sezione Identità.

Qualsiasi nuova origine dati [!DNL Audience Manager] che utilizza il tipo di ID: Cross-Device genererà uno spazio dei nomi identità corrispondente. I cookie dei tipi di ID origine dati e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi spazio nomi identità creato in Adobe Experience Platform genererà un&#39;origine dati [!DNL Audience Manager] corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio nomi.
