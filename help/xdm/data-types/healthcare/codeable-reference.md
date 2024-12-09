---
title: Tipo di dati di riferimento codificabile
description: Scopri il tipo di dati Codeable Reference Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---

# [!UICONTROL Riferimento codificabile] tipo di dati

[!UICONTROL Riferimento codificabile] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento a una risorsa o a un concetto. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati di riferimento codificabile](../../images/data-types/healthcare/codeable-reference.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Concetto] | `concept` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Un riferimento a un concetto (per classe). |
| [!UICONTROL Riferimento] | `reference` | [[!UICONTROL Riferimento]](../healthcare/reference.md) | Riferimento a una risorsa. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.schema.json)
