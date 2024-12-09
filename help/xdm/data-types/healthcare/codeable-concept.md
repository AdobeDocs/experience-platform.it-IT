---
title: Tipo di dati del concetto codificabile
description: Scopri il tipo di dati Codeable Concept Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL Concetto codificabile] tipo di dati

[!UICONTROL Concetto codificabile] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento da una risorsa a un&#39;altra. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del concetto codificabile](../../images/data-types/healthcare/codeable-concept.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codifica] | `coding` | Array di [[!UICONTROL Codifica]](../healthcare/coding.md) | Codice definito da un sistema terminologico. |
| [!UICONTROL Testo] | `text` | Stringa | Rappresentazione in testo normale del concetto. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
