---
title: Dettagli metadati personalizzati Tipo di dati di reporting
description: Scopri il tipo di dati Dettagli metadati personalizzati di Reporting Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL Dettagli metadati personalizzati] Tipo di dati di reporting

[!UICONTROL Dettagli metadati personalizzati] Il reporting è un tipo di dati Experience Data Model (XDM) standard che definisce una struttura per l’archiviazione di metadati personalizzati. Il [!UICONTROL Dettagli metadati personalizzati] Il tipo di dati di reporting acquisisce dettagli quali il nome e il valore dei metadati personalizzati associati al contenuto o alle interazioni. I servizi Adobe utilizzano i campi di reporting per contenuti multimediali per analizzare i campi di raccolta di contenuti multimediali inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

![Diagramma del tipo di dati di reporting Dettagli metadati personalizzati.](../images/data-types/the-custom-metadata-reporting.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nome campo metadati personalizzato] | `name` | string | Nome del campo personalizzato. |
| [!UICONTROL Valore campo metadati personalizzato] | `value` | string | Il valore del campo personalizzato. |

{style="table-layout:auto"}
