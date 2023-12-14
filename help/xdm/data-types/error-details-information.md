---
title: Tipo di dati informazioni dettagli errore
description: Scopri il tipo di dati Dettagli errore Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL Informazioni dettagli errore] tipo di dati

[!UICONTROL Informazioni dettagli errore] è un tipo di dati Experience Data Model (XDM) standard che descrive i dettagli dell’errore. Utilizza il [!UICONTROL Informazioni dettagli errore] tipo di dati per acquisire dettagli sull’origine dell’errore e sull’identificazione. L’ID errore identifica l’errore e la sorgente dell’errore specifica se proviene dal lettore o da una sorgente esterna.

![Diagramma del tipo di dati Informazioni dettagli errore.](../images/data-types/error-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL ID errore] | `name` | string | ID dell’errore. |
| [!UICONTROL Origine errore] | `source` | string | Origine dell’errore. Enumerato: &quot;player&quot;, &quot;external&quot; con i rispettivi significati. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
