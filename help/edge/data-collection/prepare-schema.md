---
title: Preparare lo schema XDM
seo-title: Preparare lo schema XDM
description: Guida per la creazione dello schema XDM in Adobe Experience Platform
seo-description: Guida per la creazione dello schema XDM in Adobe Experience Platform
keywords: XDM;schema;create schema;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Preparare uno schema

Il  Experience Platform Edge Network utilizza il modello dati esperienza (XDM). XDM è un formato di dati che consente di definire gli schemi. Lo schema definisce il modo in cui Edge Network prevede la formattazione dei dati. Per inviare i dati, è necessario definire lo schema.

1. [Creare uno schema](../../xdm/tutorials/create-schema-ui.md)
2. Aggiungete il [!DNL Web SDK ExperienceEvent] Mixin AEP allo schema creato.
3. Creare un dataset dallo schema creato.

Il seguente video è pensato per aiutarti a creare uno schema, un set di dati e un connettore di origine per lo streaming dei [!DNL Web SDK] dati.


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

Accedete a  Adobe Experience Platform Launch e installate l&#39;estensione AEP Web SDK. Quando installi l’SDK, ti viene richiesto di configurare l’estensione. Immettete l’ID di configurazione richiesto in precedenza. L’estensione completa automaticamente l’ID organizzazione.

Per ulteriori dettagli sulle diverse opzioni di configurazione, consulta [Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md).

[Ulteriori informazioni sulla creazione dello schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
