---
keywords: ' Experience Platform;home;temi comuni;schema;schema;XDM;profilo singolo;campi;schemi;mappe identità;mappa identità;mappa identità;schema;mappa;mappa;schema;schema unione;unione'
solution: Experience Platform
title: Mixin IdentityMap
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

>[!NOTE]
>
>I nomi di diversi mixin sono cambiati. Per ulteriori informazioni, consulta il documento relativo agli [aggiornamenti del nome del mixin](../name-updates.md).

[!UICONTROL IdentityMap] è un mixin standard per la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce un singolo campo mappa, che contiene un insieme di identità utente chiave per namespace.

>[!WARNING]
>
>Il campo `IdentityMap` viene aggiornato automaticamente dal sistema durante l&#39;acquisizione dei dati di identità. Per utilizzare correttamente questo campo per [Profilo cliente in tempo reale](../../../profile/home.md), non tentare di aggiornare manualmente il contenuto del campo nelle operazioni di dati.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Per ulteriori informazioni sul caso di utilizzo, vedere la sezione sulle mappe di identità in [funzioni di base della composizione dello schema](../../schema/composition.md#identityMap).