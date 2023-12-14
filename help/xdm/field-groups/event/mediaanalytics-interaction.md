---
title: Gruppo di campi dello schema dei dettagli dell’interazione di Media Analytics
description: Scopri il gruppo di campi dello schema Dettagli interazione di Media Analytics.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL Dettagli dell’interazione di Media Analytics] gruppo di campi schema

[!UICONTROL Dettagli dell’interazione di Media Analytics] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Utilizza questo gruppo di campi per acquisire campi di dati arricchiti che monitorano e analizzano in modo completo le interazioni con i contenuti multimediali su varie piattaforme o canali.

![Un diagramma di schema del [!UICONTROL Dettagli dell’interazione di Media Analytics] gruppo di campi dello schema.](../../images/field-groups/mediaanalytics-interaction.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---| --- | --- | --- |
| [!UICONTROL Dettagli di Media Collection] | `mediaCollection` | [[!UICONTROL Informazioni sui dettagli dei contenuti multimediali]](../../data-types/media-details-information.md) | Attributi relativi a una raccolta di elementi multimediali. |
| [!UICONTROL Dettagli di Media Reporting] | `mediaReporting` | [[!UICONTROL Informazioni sui dettagli dei contenuti multimediali]](../../data-types/media-details-information.md) | Dettagli di reporting e metriche associate al contenuto multimediale. |
| [!UICONTROL Elenco Degli Eventi Di Contenuto Scaricato Di Media Collection] | `mediaDownloadedEvents` | [!UICONTROL Array] di [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventi che tengono traccia del download di contenuti all’interno della raccolta multimediale. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
