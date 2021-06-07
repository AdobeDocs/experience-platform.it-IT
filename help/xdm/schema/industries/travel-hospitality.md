---
solution: Experience Platform
title: Settore del viaggio e dell'ospitalità Modello dati ERD
topic-legacy: overview
description: Visualizza un diagramma di relazione tra entità (ERD) che descrive un modello di dati standardizzato per il settore dei viaggi e dell’ospitalità, compatibile con Experience Data Model (XDM) per l’utilizzo in Adobe Experience Platform.
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 88c17992a391b24a76c3e387d3033df4c75a6aa6
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# [!UICONTROL Modello dati ERD per l&#39;industria ] ospedaliera e di viaggio

Il seguente diagramma di relazione tra entità (ERD) rappresenta un modello di dati standardizzato per il settore dei viaggi e dell’ospitalità. L&#39;ERD viene presentato intenzionalmente in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Adobe Experience Platform.

Utilizzare la seguente legenda per interpretare questo ERD:

* Ogni entità visualizzata in è basata su una classe [Experience Data Model (XDM) sottostante](../composition.md#class).
* Per una determinata entità, ogni riga contrassegnata in **grassetto** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito nel testo senza bolli.
* I campi più importanti per una determinata entità sono evidenziati in rosso.
* Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.
* Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>L&#39;entità Experience Event include un campo &quot;_ID&quot; che rappresenta l&#39;attributo di identificatore univoco (`_id`) fornito dalla classe ExperienceEvent XDM. Per ulteriori informazioni su ciò che ci si aspetta da questo valore, consulta il documento di riferimento su [XDM ExperienceEvent](../../classes/experienceevent.md) .