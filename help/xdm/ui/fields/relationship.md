---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;relationship;field;
solution: Experience Platform
title: Definire un campo di relazione nell'interfaccia utente
description: Scoprite come definire un campo di relazione nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Definire un campo di relazione nell&#39;interfaccia utente

In Experience Data Model (XDM), uno [schema unione](../../schema/composition.md#union) è una visualizzazione unificata di tutti gli schemi appartenenti alla stessa classe che sono stati abilitati anche per [Real-time Customer Profile](../../../profile/home.md). Lo schema unione è basato su Profile per creare una rappresentazione completa di un cliente da dati esperienza diversi.

In alcuni casi, è possibile che si stiano assimilando dati che non fanno necessariamente parte di un profilo, ma che sono comunque correlati al profilo. Un esempio di questo tipo di dati sarebbe un campo &quot;hotel preferito&quot; per un cliente. Poiché gli attributi dell&#39;hotel preferito di una persona non sono attributi della persona stessa, un hotel è rappresentato meglio da uno schema separato basato su una classe personalizzata piuttosto che [!DNL XDM Individual Profile].

Poiché gli schemi di unione sono basati solo su schemi che condividono la stessa classe, l&#39;abilitazione dello schema &quot;Hotels&quot; per l&#39;utilizzo in Profile non includerà lo schema di unione dei campi per [!DNL XDM Individual Profile]. Al contrario, è necessario definire una relazione tra &quot;Hotels&quot; e un altro schema appartenente all&#39;unione. Ciò comporta la definizione di un campo di relazione **a1/> in uno schema di origine che fa riferimento all&#39;identità primaria di uno schema di destinazione.**

Per i passaggi dettagliati sulla definizione di una relazione tra due schemi nell&#39;interfaccia utente di Adobe Experience Platform, consultate l&#39;esercitazione sull&#39;interfaccia utente delle [relazioni](../../tutorials/relationship-ui.md).