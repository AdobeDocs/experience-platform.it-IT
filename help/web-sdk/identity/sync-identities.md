---
title: Sincronizzazione delle identità tra Audienci Manager e Adobe Experience Platform tramite Platform Web SDK
description: Scopri come sincronizzare le identità tra Audienci Manager e Adobe Experience Platform utilizzando Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identità;sincronizzare identità;namespace;
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Sincronizzazione delle identità tra Audienci Manager e Experienci Platform

Adobe Experience Platform Web SDK supporta la capacità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite [sendEvent](./overview.md#syncing-identities) comando.

Scegli i namespace dalla [Namespace di Identity Service](../../identity/../identity-service/features/namespaces.md) per indicare il contesto a cui si riferisce un’identità, utilizzando i valori nella colonna Simbolo di identità:

![Visualizzazione dell’interfaccia utente Namespace](../assets/identity/edge_namespaceUI_identity-symbol.png)

Come cliente Audience Manager, tutte le origini dati esistenti che utilizzano il tipo ID: multi-dispositivo hanno automaticamente uno spazio dei nomi di identità corrispondente. Per trovare il namespace Identity corrispondente all’origine dati di Audience Manager, accedi a Adobe Experience Platform e passa alla sezione Identities.

Qualsiasi nuovo [!DNL Audience Manager] Origine dati che utilizza il tipo ID: multi-dispositivo genererà uno spazio dei nomi di identità corrispondente. I tipi di ID sorgente dati Cookie e ID Device Advertising non sono attualmente supportati. Inoltre, qualsiasi spazio dei nomi di identità creato in Adobe Experience Platform genererà un [!DNL Audience Manager] Origine dati ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio dei nomi.
