---
title: Invio di dati ad Adobe Audience Manager
seo-title: Invio di dati ad Adobe Audience Manager con Adobe Experience Platform Web SDK
description: Scopri come inviare dati ad Adobe Audience Manager con  Experience Platform Web SDK
seo-description: Scopri come inviare dati ad Adobe Audience Manager con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: b87b1f8a979e028c5ebf57cecf0213a075df90a6
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# [!DNL Audience Manager] sulla [!DNL Experience Platform Edge Network]

L’Adobe Experience Platform [!DNL Web SDK] è integrato con Adobe Audience Manager e supporta l’invio e la ricezione di dati da destinazioni [!DNL Audience Manager], cookie e URL e sincronizzazione ID.

## Abilitazione [!DNL Audience Manager]

Per abilitare [!DNL Audience Manager] dovrete effettuare le seguenti operazioni:

- Abilitate [!DNL Audience Manager] la configurazione [](../../fundamentals/edge-configuration.md)edge.
- Abilita o disabilita cookie e destinazioni URL.
- Specifica del contenitore di sincronizzazione ID per le sincronizzazioni di partner esterni (facoltativo)

## Identità di sincronizzazione

Adobe Experience Platform Web SDK supporta la possibilità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite il comando [sendEvent](../../fundamentals/identity.md#syncing-identities) .

Scegliete gli spazi dei nomi dagli spazi dei nomi del servizio [identità](../../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità, utilizzando i valori nella colonna Simbolo di identità:

![Visualizzazione dell’interfaccia utente Spazi dei nomi](../../../assets/edge_namespaceUI_identity-symbol.png)

Come cliente di  Audience Manager, tutte le tue Origini dati esistenti che utilizzano il tipo di ID: Cross-Device dispone automaticamente di uno spazio dei nomi identità corrispondente. Per trovare lo spazio dei nomi identità corrispondente per l&#39;origine dati  Audience Manager, accedere all&#39;Adobe Experience Platform e passare alla sezione Identità.

Qualsiasi nuova origine [!DNL Audience Manager] dati che utilizza il tipo di ID: Cross-Device genererà uno spazio dei nomi identità corrispondente. I cookie dei tipi di ID origine dati e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi spazio nomi identità creato in Adobe Experience Platform genererà un&#39;origine [!DNL Audience Manager] dati corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio nomi.
