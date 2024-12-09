---
title: Tipo di dati del rapporto
description: Scopri il tipo di dati Ratio Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Rapporto] tipo di dati

[!UICONTROL Ratio] è un tipo di dati XDM (Experience Data Model) standard che fornisce un rapporto di due valori [[!UICONTROL Quantity]](../healthcare/quantity.md) tramite un numeratore e un denominatore. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del rapporto](../../images/data-types/healthcare/ratio.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Denominatore] | `denominator` | [[!UICONTROL Quantità semplice]](../healthcare/simple-quantity.md) | Il valore del denominatore. |
| [!UICONTROL Numeratore] | `numerator` | [[!UICONTROL Quantità]](../healthcare/quantity.md) | Il valore del numeratore. |

>[!NOTE]
>
> `denominator` e `numerator` hanno tipi di dati diversi a causa della specifica creata in base alla versione 5 di HL7 FHIR.

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
