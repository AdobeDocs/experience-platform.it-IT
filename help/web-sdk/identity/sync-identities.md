---
title: Sincronizzazione delle identità tra Audience Manager e Adobe Experience Platform tramite Experience Platform Web SDK
description: Scopri come sincronizzare le identità tra Audience Manager e Adobe Experience Platform utilizzando Experience Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identità;sincronizzare identità;namespace;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Sincronizzazione delle identità tra Audience Manager e Experience Platform

Adobe Experience Platform Web SDK supporta la possibilità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite il comando [sendEvent](./overview.md#syncing-identities).

Scegli i tuoi spazi dei nomi da [Spazi dei nomi del servizio Identity](../../identity/../identity-service/features/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità, utilizzando i valori nella colonna Simbolo identità:

![Visualizzazione dell&#39;interfaccia utente degli spazi dei nomi](../assets/identity/edge_namespaceUI_identity-symbol.png)

In qualità di cliente di Audience Manager, tutte le origini dati esistenti che utilizzano il tipo ID: multidispositivo dispongono automaticamente di uno spazio dei nomi di identità corrispondente. Per trovare il namespace Identity corrispondente per Audience Manager Data Source, accedi a Adobe Experience Platform e passa alla sezione Identities.

Qualsiasi nuovo Data Source [!DNL Audience Manager] che utilizza il tipo ID: Cross-Device genererà uno spazio dei nomi di identità corrispondente. Cookie e ID dispositivo di Source Advertising ID dei tipi di dati non sono attualmente supportati. Inoltre, qualsiasi spazio dei nomi di identità creato in Adobe Experience Platform genererà un Source dati [!DNL Audience Manager] corrispondente. Tuttavia, il metodo syncIdentity supporta solo i simboli di identità dello spazio dei nomi.
