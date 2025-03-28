---
title: Tipo di dati intervallo
description: Scopri il tipo di dati Range Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 66f8b574-04d9-435f-8743-4ff89c4c0079
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 8%

---

# Tipo di dati [!UICONTROL Range]

[!UICONTROL Intervallo] è un tipo di dati XDM (Experience Data Model) standard che fornisce un set di valori associati a valori minimi e massimi. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura tipo di dati intervallo](../../../images/healthcare/data-types/range.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Alta] | `high` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | Il limite più alto. |
| [!UICONTROL Basso] | `low` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | Il limite più basso. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/range.schema.json)
