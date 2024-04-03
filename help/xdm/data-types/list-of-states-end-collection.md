---
title: Elenco degli stati Tipo di dati di raccolta finale
description: Scopri il tipo di dati List of States End Collection Data Type (XDM).
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL Fine elenco di stati] tipo di dati

Il tipo di dati List of States End Collection è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato finale di vari attributi del lettore. Include [!UICONTROL Nome stato lettore] proprietà che indica lo stato specifico dell’attributo (ad esempio, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Diagramma del tipo di dati Fine raccolta elenco stati.](../images/data-types/list-of-states-end-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome stato lettore] | `name` | string | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
