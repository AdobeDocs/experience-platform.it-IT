---
title: Tipo di dati money
description: Scopri il tipo di dati Money Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b910a45-01d5-404b-9710-a2fad9885452
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 18%

---

# Tipo di dati [!UICONTROL Money]

[!UICONTROL Money] è un tipo di dati XDM (Experience Data Model) standard che fornisce una quantità di utilità economica in una valuta riconosciuta. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati Money](../../../images/healthcare/data-types/money.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Valuta] | `currency` | Stringa | Il codice valuta ISO 4217. |
| [!UICONTROL Valore] | `value` | Doppio | Il valore numerico. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/money.schema.json)
