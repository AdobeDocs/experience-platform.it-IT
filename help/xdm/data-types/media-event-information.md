---
title: Tipo di dati informazioni evento multimediale
description: Scopri il tipo di dati Media Event Information Experience Data Model (XDM).
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL Informazioni evento multimediale] tipo di dati

[!UICONTROL Informazioni evento multimediale] è un tipo di dati Experience Data Model (XDM) standard che descrive le informazioni dei dettagli multimediali relative all’evento esperienza.

![Un diagramma del tipo di dati Informazioni evento multimediale.](../images/data-types/media-event-information.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | Informazioni sui dettagli dei contenuti multimediali relative all’evento esperienza. Questo tipo di dati viene utilizzato per entrambi [raccolta dati multimediali](./media-collection-details.md) e [reportistica di dati multimediali](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL Stringa] | L’ora in cui si è verificato un evento multimediale. |
| `mediaEventType` | [!UICONTROL Stringa] | Il tipo di evento multimediale. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)
