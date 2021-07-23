---
title: Sincronizzazione delle identità tra Audience Manager e Adobe Experience Platform tramite l’SDK per web di Platform
description: Scopri come sincronizzare le identità tra Audience Manager e Adobe Experience Platform utilizzando Platform Web SDK
seo-description: Scopri come sincronizzare le identità con Adobe Audience Manager con Experience Platform Web SDK
keywords: audience manager;aam;identità;identità di sincronizzazione;spazio dei nomi;
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Sincronizzazione delle identità tra Audience Manager e Experience Platform

Adobe Experience Platform Web SDK supporta la possibilità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite il comando [sendEvent](./overview.md#syncing-identities) .

Scegli i namespace da [Namespace del servizio Identity](../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un’identità, utilizzando i valori nella colonna Simbolo di identità:

![Visualizzazione dell’interfaccia utente dei namespace](../images/identity/edge_namespaceUI_identity-symbol.png)

In qualità di cliente di Audience Manager, tutte le tue origini dati esistenti che utilizzano il tipo di ID: Cross-Device dispone automaticamente di uno spazio dei nomi identità corrispondente. Per trovare lo spazio dei nomi identità corrispondente per l’origine dati Audience Manager, accedi a Adobe Experience Platform e passa alla sezione Identità .

Qualsiasi nuova origine dati [!DNL Audience Manager] che utilizza il tipo ID: Cross-Device genera uno spazio dei nomi di identità corrispondente. Tipi di ID origine dati I cookie e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi namespace Identity creato in Adobe Experience Platform genererà un’origine dati [!DNL Audience Manager] corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio dei nomi.
