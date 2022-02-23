---
title: Tipo di dati coppia valore chiave
description: Questo documento fornisce una panoramica del tipo di dati XDM (Key Value Pair Experience Data Model).
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL Coppia di valori chiave] tipo di dati

[!UICONTROL Coppia di valori chiave] è un tipo di dati XDM (Experience Data Model) standard che acquisisce i dettagli di una coppia chiave-valore generica. Questo tipo di dati viene utilizzato nella [[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] gruppo di campi](../field-groups/event/analytics-full-extension.md) per descrivere gli elementi della matrice di una variabile di elenco.

![Struttura della coppia di valori chiave](../images/data-types/key-value-pair.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `key` | Stringa | Una chiave (nome) per una variabile o un valore generico. |
| `value` | Stringa | Il valore della variabile. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
