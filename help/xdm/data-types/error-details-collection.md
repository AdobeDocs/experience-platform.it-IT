---
title: Tipo di dati raccolta dettagli errore
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli degli errori.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 12%

---

# [!UICONTROL Dettagli errore] Tipo di dati raccolta

[!UICONTROL Dettagli errore] La raccolta è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli dell&#39;errore. Utilizza il tipo di dati della raccolta [!UICONTROL Dettagli errore] per acquisire i dettagli dell&#39;origine e dell&#39;identificazione dell&#39;errore. L’ID errore identifica l’errore e la sorgente dell’errore specifica se proviene dal lettore o da una sorgente esterna.

![Diagramma del tipo di dati Informazioni dettagli errore.](../images/data-types/error-details-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL ID errore] | `name` | stringa | No | ID dell’errore. |
| [!UICONTROL Errore Source] | `source` | stringa | No | Origine dell’errore. Enumerato: &quot;player&quot;, &quot;external&quot; con i rispettivi significati. |

{style="table-layout:auto"}
