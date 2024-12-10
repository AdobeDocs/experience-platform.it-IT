---
title: Tipo di dati periodo
description: Scopri il tipo di dati Period Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 10%

---

# Tipo di dati [!UICONTROL Periodo]

[!UICONTROL Periodo] è un tipo di dati XDM (Experience Data Model) standard che fornisce un periodo di tempo definito da una data/ora di inizio e di fine. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati periodo](../../../images/healthcare/data-types/period.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Fine] | `end` | Data e ora | La data e l’ora di fine. |
| [!UICONTROL Inizio] | `start` | Data e ora | La data e l’ora di inizio. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)
