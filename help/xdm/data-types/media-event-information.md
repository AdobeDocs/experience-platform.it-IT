---
title: Tipo di dati informazioni evento multimediale
description: Scopri il tipo di dati Media Event Information Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL Informazioni evento multimediale] tipo di dati

[!UICONTROL Informazioni evento multimediale] è un tipo di dati Experience Data Model (XDM) standard che descrive le informazioni dei dettagli multimediali relative all’evento esperienza.

![Un diagramma del tipo di dati Informazioni evento multimediale.](../images/data-types/media-event-information.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | Informazioni sui dettagli dei contenuti multimediali relative all’evento esperienza. |
| `mediaEventTimestamp` | [!UICONTROL Stringa] | L’ora in cui si è verificato un evento multimediale. |
| `mediaEventType` | [!UICONTROL Stringa] | Il tipo di evento multimediale. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
