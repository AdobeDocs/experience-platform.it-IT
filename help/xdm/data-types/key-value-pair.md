---
title: Tipo di dati coppia di valori chiave
description: Scopri il tipo di dati Experience Data Model (XDM) della coppia di valori chiave.
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 5%

---

# [!UICONTROL Coppia chiave-valore] tipo di dati

[!UICONTROL Coppia chiave-valore] è un tipo di dati Experience Data Model (XDM) standard che acquisisce i dettagli di una coppia chiave-valore generica. Questo tipo di dati viene utilizzato in [[!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] gruppo di campi](../field-groups/event/analytics-full-extension.md) per descrivere gli elementi array di una variabile elenco.

![Struttura della coppia di valori chiave](../images/data-types/key-value-pair.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `key` | Stringa | Chiave (nome) per una variabile o un valore generico. |
| `value` | Stringa | Il valore della variabile. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta [l’archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).
