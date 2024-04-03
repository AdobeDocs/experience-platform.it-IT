---
title: Gruppo di campi dello schema dei dettagli dell’interazione di Media Analytics
description: Scopri il gruppo di campi dello schema Dettagli interazione di Media Analytics.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL Dettagli dell’interazione di Media Analytics] gruppo di campi schema

[!UICONTROL Dettagli dell’interazione di Media Analytics] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Utilizza questo gruppo di campi per acquisire campi di dati arricchiti che monitorano e analizzano in modo completo le interazioni con i contenuti multimediali su varie piattaforme o canali.

![Un diagramma di schema del [!UICONTROL Dettagli dell’interazione di Media Analytics] gruppo di campi dello schema.](../../images/field-groups/mediaanalytics-interaction.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|---| --- | --- | --- |
| [!UICONTROL Dettagli di Media Collection] | `mediaCollection` | [[!UICONTROL Dettagli di Media Collection]](../../data-types/media-collection-details.md) | Attributi relativi a una raccolta di elementi multimediali. Utilizza i campi Media Collection per acquisire dati e inviarli ad altri servizi Adobe per l’ulteriore elaborazione. |
| [!UICONTROL Dettagli di Media Reporting] | `mediaReporting` | [[!UICONTROL Dettagli di Media Reporting]](../../data-types/media-reporting-details.md) | Dettagli di reporting e metriche associate al contenuto multimediale. * I campi Media Reporting vengono utilizzati dai servizi Adobe per analizzare i campi Media Collection inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati. |
| [!UICONTROL Elenco Degli Eventi Di Contenuto Scaricato Di Media Collection] | `mediaDownloadedEvents` | [!UICONTROL Array] di [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Eventi che tengono traccia del download di contenuti all’interno della raccolta multimediale. |

{style="table-layout:auto"}

>[!TIP]
>
>Puoi nascondere i campi non utilizzati dall’API Media Edge. Nascondere questi campi semplifica la lettura e la comprensione dello schema, ma non è obbligatorio. Questi campi si riferiscono solo a quelli [!UICONTROL Dettagli dell’interazione di Media Analytics] gruppo di campi. Per migliorare la leggibilità nell’interfaccia utente di Platform, segui le istruzioni in [Documentazione di Media Analytics su come nascondere i campi non utilizzati](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
