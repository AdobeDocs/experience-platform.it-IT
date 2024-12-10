---
title: Tipo di dati del concetto codificabile
description: Scopri il tipo di dati Codeable Concept Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: c172a7cd-24c6-484b-8552-8745dfd3a8e9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 9%

---

# [!UICONTROL Concetto codificabile] tipo di dati

[!UICONTROL Concetto codificabile] è un tipo di dati XDM (Experience Data Model) standard che descrive un riferimento da una risorsa a un&#39;altra. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del concetto codificabile](../../../images/healthcare/data-types/codeable-concept.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codifica] | `coding` | Array di [[!UICONTROL Codifica]](../data-types/coding.md) | Codice definito da un sistema terminologico. |
| [!UICONTROL Testo] | `text` | Stringa | Rappresentazione in testo normale del concetto. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeablereference.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/codeableconcept.schema.json)
