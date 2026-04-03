---
title: Elenco degli stati Tipo di dati di raccolta finale
description: Scopri il tipo di dati List of States End Collection Data Type (XDM).
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 7%

---

# Tipo di dati [!UICONTROL List of States End]

Il tipo di dati List of States End Collection è un tipo di dati Experience Data Model (XDM) progettato per rappresentare informazioni relative allo stato finale di vari attributi del lettore. Include le proprietà [!UICONTROL Player State Name] che indicano lo stato specifico dell&#39;attributo (ad esempio, &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). Questo tipo di dati viene utilizzato per acquisire e descrivere le condizioni iniziali di diversi stati del lettore.

![Diagramma del tipo di dati Fine raccolta dell&#39;elenco degli stati.](../images/data-types/list-of-states-end-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL Player State Name] | `name` | stringa | No | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |

{style="table-layout:auto"}
