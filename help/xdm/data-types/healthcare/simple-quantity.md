---
title: Tipo di dati Quantità semplice
description: Scopri il tipo di dati Simple Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---

# [!UICONTROL Quantità semplice] tipo di dati

[!UICONTROL Simple Quantity] è un tipo di dati XDM (Experience Data Model) standard che fornisce una quantità misurata o misurabile. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura tipo dati Quantità semplice](../../images/data-types/healthcare/simple-quantity.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | Stringa | La forma codificata dell’unità. |
| [!UICONTROL Sistema] | `system` | Stringa | Sistema che definisce il formato di unità codificata, rappresentato come URI. |
| [!UICONTROL Unità] | `unit` | Stringa | La rappresentazione dell’unità. |
| [!UICONTROL Valore] | `value` | Doppio | Il valore numerico. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/simplequantity.schema.json)
