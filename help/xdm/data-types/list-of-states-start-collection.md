---
title: Elenco degli stati - Avvia tipo di dati raccolta
description: Scopri il tipo di dati XDM (Experience Data Model) dell’elenco degli stati.
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL Tipo di dati Inizio elenco stati]

Il tipo di dati [!UICONTROL Elenco stati inizio] è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato iniziale di vari attributi del lettore. Include le proprietà [!UICONTROL Nome stato lettore] che indicano lo stato dell&#39;attributo specifico, ad esempio &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;. Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Diagramma di [!UICONTROL Tipo di dati Inizio elenco stati].](../images/data-types/list-of-states-start-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Nome stato lettore] | `name` | stringa | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
