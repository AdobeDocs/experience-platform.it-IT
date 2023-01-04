---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;relazione;campo;
solution: Experience Platform
title: Definire i campi di relazione nell’interfaccia utente
description: Scopri come definire un campo di relazione nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definire i campi delle relazioni nell’interfaccia utente

In Experience Data Model (XDM), un [schema unione](../../schema/composition.md#union) è una visualizzazione unificata di tutti gli schemi appartenenti alla stessa classe abilitati anche per [Profilo cliente in tempo reale](../../../profile/home.md). Lo schema di unione viene sfruttato da Profilo per creare una rappresentazione completa di un cliente da dati di esperienza diversi.

In alcuni casi, potresti acquisire dati che non fanno necessariamente parte di un profilo, ma che sono comunque correlati al profilo. Un esempio di questo tipo di dati sarebbe un campo &quot;hotel preferito&quot; per un cliente. Poiché gli attributi dell&#39;hotel preferito di una persona non sono attributi della persona stessa, un hotel è rappresentato al meglio da uno schema separato basato su una classe personalizzata piuttosto che da [!DNL XDM Individual Profile].

Poiché gli schemi di unione sono basati solo su schemi che condividono la stessa classe, semplicemente abilitando lo schema &quot;Hotels&quot; per l’utilizzo in Profile non verrà incluso lo schema di unione dei campi per [!DNL XDM Individual Profile]. Al contrario, devi definire una relazione tra &quot;Hotel&quot; e un altro schema appartenente all&#39;unione. Ciò comporta la definizione di un **campo di relazione** in uno schema di origine che fa riferimento all&#39;identità principale di uno schema di destinazione.

Per i passaggi dettagliati sulla definizione di una relazione tra due schemi nell’interfaccia utente di Adobe Experience Platform, consulta la sezione [esercitazione sulla relazione UI](../../tutorials/relationship-ui.md).
