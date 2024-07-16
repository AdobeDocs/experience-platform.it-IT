---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;relationship;field;
solution: Experience Platform
title: Definire i campi di relazione nell’interfaccia utente
description: Scopri come definire un campo di relazione nell’interfaccia utente di Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definire i campi di relazione nell’interfaccia utente

In Experience Data Model (XDM), uno [schema di unione](../../schema/composition.md#union) è una visualizzazione unificata di tutti gli schemi appartenenti alla stessa classe abilitati anche per [Profilo cliente in tempo reale](../../../profile/home.md). Lo schema di unione viene utilizzato dal profilo per creare una rappresentazione completa di un cliente a partire da dati di esperienza diversi.

In alcuni casi, è possibile che si acquisiscano dati che non fanno necessariamente parte di un profilo, ma che sono comunque correlati al profilo. Un esempio di questo tipo di dati sarebbe il campo &quot;hotel preferito&quot; per un cliente. Poiché gli attributi dell&#39;hotel preferito di una persona non sono attributi della persona stessa, un hotel è meglio rappresentato da uno schema separato basato su una classe personalizzata anziché [!DNL XDM Individual Profile].

Poiché gli schemi di unione sono basati solo su schemi che condividono la stessa classe, la semplice attivazione dello schema &quot;Hotels&quot; per l&#39;utilizzo nel profilo non includerà lo schema di unione dei campi per [!DNL XDM Individual Profile]. Invece, devi definire una relazione tra &quot;Hotel&quot; e un altro schema appartenente all’unione. Ciò comporta la definizione di un **campo relazione** in uno schema di origine che fa riferimento all&#39;identità primaria di uno schema di riferimento.

Per i passaggi dettagliati sulla definizione di una relazione tra due schemi nell&#39;interfaccia utente di Adobe Experience Platform, consulta l&#39;esercitazione sull&#39;interfaccia utente delle [relazioni](../../tutorials/relationship-ui.md).
