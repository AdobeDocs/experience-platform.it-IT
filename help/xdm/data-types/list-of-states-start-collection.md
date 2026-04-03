---
title: Elenco degli stati - Avvia tipo di dati raccolta
description: Scopri il tipo di dati XDM (Experience Data Model) dell’elenco degli stati.
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 8%

---

# Tipo di dati [!UICONTROL List of States Start]

Il tipo di dati [!UICONTROL List of States Start] è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato iniziale di vari attributi del lettore. Include le proprietà [!UICONTROL Player State Name] che indicano lo stato specifico dell&#39;attributo (ad esempio, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Diagramma del tipo di dati [!UICONTROL List of States Start].](../images/data-types/list-of-states-start-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | stringa | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
