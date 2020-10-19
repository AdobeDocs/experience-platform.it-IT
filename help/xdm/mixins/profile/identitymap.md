---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Mixin IdentityMap
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# [!UICONTROL IdentityMap] mixin

[!UICONTROL IdentityMap] è un mixin standard per la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il mixin fornisce un singolo campo mappa, che contiene un insieme di identità utente chiave per namespace.

>[!WARNING]
>
>Il `IdentityMap` campo viene aggiornato automaticamente dal sistema durante l&#39;acquisizione dei dati di identità. Per utilizzare correttamente questo campo per il profilo [cliente in tempo](../../../profile/home.md)reale, non tentare di aggiornare manualmente il contenuto del campo nelle operazioni di dati.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Per ulteriori informazioni sul caso di utilizzo, vedere la sezione sulle mappe di identità nelle [nozioni di base della composizione](../../schema/composition.md#identityMap) dello schema.