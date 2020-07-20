---
title: Invio di dati a  Adobe Audience Manager
seo-title: Invio di dati a  Adobe Audience Manager con  Adobe Experience Platform Web SDK
description: Scopri come inviare dati a  Adobe Audience Manager con  Experience Platform Web SDK
seo-description: Scopri come inviare dati a  Adobe Audience Manager con  Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# [!DNL Audience Manager] sulla [!DNL Experience Platform Edge Network]

Il Adobe Experience Platform  [!DNL Web SDK] è integrato con  Adobe Audience Manager e supporta l’invio e la ricezione di dati da destinazioni [!DNL Audience Manager], cookie e URL e sincronizzazione ID.

## Abilitazione [!DNL Audience Manager]

Per abilitare [!DNL Audience Manager] dovrete effettuare le seguenti operazioni:

- Abilitate [!DNL Audience Manager] la configurazione [](../../fundamentals/edge-configuration.md)edge.
- Abilita o disabilita cookie e destinazioni URL.
- Specifica del contenitore di sincronizzazione ID per le sincronizzazioni di partner esterni (facoltativo)

## Identità di sincronizzazione

Il Adobe Experience Platform  [!DNL Web SDK] supporta la possibilità di dichiarare gli ID cliente e i relativi stati di autenticazione tramite il comando [SyncIdentity](../../fundamentals/identity.md) .

Il metodo syncIdentity utilizza gli spazi dei nomi del servizio [identità](../../../identity/../identity-service/namespaces.md) per indicare il contesto a cui si riferisce un&#39;identità. In qualità di [!DNL Audience Manager] cliente, tutte le tue Origini dati esistenti che utilizzano il tipo di ID: Cross-Device avrà automaticamente una corrispondente [!DNL Identity Namespace]. Per trovare il corrispondente [!DNL Identity Namespace] per il vostro [!DNL Audience Manager Data Source], accedete al Adobe Experience Platform  e andate alla [!DNL Identities] sezione.

![Visualizzazione dell’interfaccia utente Spazi dei nomi](../../../assets/edge_configuration_identity.png)

Qui puoi cercare la tua Origine [!DNL Audience Manager] dati per Nome. Il metodo syncIdentity utilizza il simbolo di identità per specificare lo spazio dei nomi.

Qualsiasi nuova origine [!DNL Audience Manager] dati che utilizza il tipo di ID: Cross-Device genererà uno spazio dei nomi identità corrispondente. I cookie dei tipi di ID origine dati e l&#39;ID pubblicità dispositivo non sono attualmente supportati. Inoltre, qualsiasi spazio nomi identità creato in  Adobe Experience Platform genererà un&#39;origine [!DNL Audience Manager] dati corrispondente, ma si noti che il metodo syncIdentity supporta solo i simboli di identità dello spazio nomi.
