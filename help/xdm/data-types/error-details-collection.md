---
title: Tipo di dati raccolta dettagli errore
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli degli errori.
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Dettagli errore] Tipo di dati della raccolta

[!UICONTROL Dettagli errore] La raccolta è un tipo di dati Experience Data Model (XDM) standard che descrive i dettagli dell’errore. Utilizza il [!UICONTROL Dettagli errore] Tipo di dati della raccolta per acquisire dettagli sull’origine dell’errore e sull’identificazione. L’ID errore identifica l’errore e la sorgente dell’errore specifica se proviene dal lettore o da una sorgente esterna.

![Diagramma del tipo di dati Informazioni dettagli errore.](../images/data-types/error-details-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID errore] | `name` | string | No | ID dell’errore. |
| [!UICONTROL Origine errore] | `source` | string | No | Origine dell’errore. Enumerato: &quot;player&quot;, &quot;external&quot; con i rispettivi significati. |

{style="table-layout:auto"}
