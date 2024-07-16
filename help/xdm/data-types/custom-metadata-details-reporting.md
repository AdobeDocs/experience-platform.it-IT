---
title: Dettagli metadati personalizzati Tipo di dati di reporting
description: Scopri il tipo di dati Dettagli metadati personalizzati di Reporting Experience Data Model (XDM).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# [!UICONTROL Dettagli metadati personalizzati] Tipo di dati di reporting

[!UICONTROL Dettagli metadati personalizzati] Il reporting è un tipo di dati Experience Data Model (XDM) standard che definisce una struttura per l&#39;archiviazione di metadati personalizzati. Il tipo di dati per la generazione di rapporti [!UICONTROL Dettagli metadati personalizzati] acquisisce dettagli quali il nome e il valore dei metadati personalizzati associati al contenuto o alle interazioni. I servizi Adobe utilizzano i campi di reporting per contenuti multimediali per analizzare i campi di raccolta di contenuti multimediali inviati dagli utenti. Questi dati, insieme ad altre metriche utente specifiche, vengono calcolati e segnalati.

![Diagramma del tipo di dati di report Dettagli metadati personalizzati.](../images/data-types/the-custom-metadata-reporting.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Nome campo metadati personalizzato] | `name` | stringa | Nome del campo personalizzato. |
| [!UICONTROL Valore Campo Metadati Personalizzato] | `value` | stringa | Il valore del campo personalizzato. |

{style="table-layout:auto"}
