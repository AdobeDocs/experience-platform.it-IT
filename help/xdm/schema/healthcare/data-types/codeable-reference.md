---
title: Tipo di dati di riferimento codificabile
description: Scopri il tipo di dati Codeable Reference Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5ac4bc82-3c8e-4622-8a4e-c954bd6e6411
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL Riferimento codificabile] tipo di dati

[!UICONTROL Riferimento codificabile] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento a una risorsa o a un concetto. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati di riferimento codificabile](../../../images/healthcare/data-types/codeable-reference.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Concetto] | `concept` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Un riferimento a un concetto (per classe). |
| [!UICONTROL Riferimento] | `reference` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Riferimento a una risorsa. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
