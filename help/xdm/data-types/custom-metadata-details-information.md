---
title: Tipo di dati dettagli metadati personalizzati
description: Scopri il tipo di dati Dettagli metadati personalizzati di Experience Data Model (XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL Informazioni sui dettagli dei metadati personalizzati] tipo di dati

[!UICONTROL Informazioni sui dettagli dei metadati personalizzati] è un tipo di dati Experience Data Model (XDM) standard che definisce una struttura per l’archiviazione di metadati personalizzati. Utilizza il [!UICONTROL Informazioni sui dettagli dei metadati personalizzati] tipo di dati per acquisire dettagli quali il nome e il valore dei metadati personalizzati associati al contenuto o alle interazioni.

![Diagramma del tipo di dati Dettagli metadati personalizzati.](../images/data-types/custom-metadata-details-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nome campo metadati personalizzato] | `name` | string | Nome del campo personalizzato. |
| [!UICONTROL Valore campo metadati personalizzato] | `value` | string | Il valore del campo personalizzato. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
