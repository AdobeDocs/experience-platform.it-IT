---
title: Elenco degli stati Tipo di dati di raccolta finale
description: Scopri il tipo di dati List of States End Collection Data Type (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL Tipo di dati Fine elenco stati]

Il tipo di dati List of States End Collection è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato finale di vari attributi del lettore. Include le proprietà [!UICONTROL Nome stato lettore] che indicano lo stato dell&#39;attributo specifico, ad esempio &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;. Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Diagramma del tipo di dati Fine raccolta dell&#39;elenco degli stati.](../images/data-types/list-of-states-end-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome stato lettore] | `name` | stringa | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
