---
title: Elenco degli stati - Avvia tipo di dati raccolta
description: Scopri il tipo di dati XDM (Experience Data Model) dell’elenco degli stati.
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 5%

---

# [!UICONTROL Inizio elenco degli stati] tipo di dati

Il [!UICONTROL Inizio elenco degli stati] tipo di dati è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato iniziale di vari attributi del lettore. Include [!UICONTROL Nome stato lettore] proprietà che indica lo stato specifico dell’attributo (ad esempio, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Un diagramma di [!UICONTROL Inizio elenco degli stati] tipo di dati.](../images/data-types/list-of-states-start-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome stato lettore] | `name` | string | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
