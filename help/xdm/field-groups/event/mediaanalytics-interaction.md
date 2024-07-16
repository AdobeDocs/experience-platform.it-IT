---
title: Gruppo di campi dello schema dei dettagli dell’interazione di Media Analytics
description: Scopri il gruppo di campi dello schema Dettagli interazione di Media Analytics.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 2%

---

# [!UICONTROL Dettagli interazione MediaAnalytics] gruppo di campi schema

[!UICONTROL Dettagli interazione MediaAnalytics] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Utilizza questo gruppo di campi per acquisire campi di dati arricchiti che monitorano e analizzano in modo completo le interazioni con i contenuti multimediali su varie piattaforme o canali.

![Diagramma di schema del gruppo di campi dello schema [!UICONTROL Dettagli interazione di MediaAnalytics].](../../images/field-groups/mediaanalytics-interaction.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---| --- | --- | --- |
| [!UICONTROL Dettagli raccolta file multimediali] | `mediaCollection` | [[!UICONTROL Dettagli raccolta file multimediali]](../../data-types/media-collection-details.md) | Attributi relativi a una raccolta di elementi multimediali. Utilizza i campi Media Collection per acquisire dati e inviarli ad altri servizi Adobe per l’ulteriore elaborazione. |
| [!UICONTROL Dettagli report multimediali] | `mediaReporting` | [[!UICONTROL Dettagli report multimediali]](../../data-types/media-reporting-details.md) | Dettagli di reporting e metriche associate al contenuto multimediale. * I campi Media Reporting vengono utilizzati dai servizi Adobe per analizzare i campi Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati. |
| [!UICONTROL Elenco Degli Eventi Di Contenuto Scaricato Di Media Collection] | `mediaDownloadedEvents` | [!UICONTROL Array] di [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventi che tengono traccia del download di contenuti all’interno della raccolta multimediale. |

{style="table-layout:auto"}

>[!TIP]
>
>Puoi nascondere i campi non utilizzati dall’API Media Edge. Nascondere questi campi semplifica la lettura e la comprensione dello schema, ma non è obbligatorio. Questi campi fanno riferimento solo a quelli del gruppo di campi [!UICONTROL Dettagli interazione MediaAnalytics]. Per migliorare la leggibilità nell&#39;interfaccia utente di Platform, segui le istruzioni riportate nella [documentazione di Media Analytics su come nascondere i campi inutilizzati](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
