---
title: Tipo di dati del rapporto
description: Scopri il tipo di dati Ratio Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8b530af6-0e64-4c30-a7d7-eb221b0b6181
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 6%

---

# [!UICONTROL Rapporto] tipo di dati

[!UICONTROL Ratio] è un tipo di dati XDM (Experience Data Model) standard che fornisce un rapporto di due valori [[!UICONTROL Quantity]](../data-types/quantity.md) tramite un numeratore e un denominatore. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del rapporto](../../../images/healthcare/data-types/ratio.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Denominatore] | `denominator` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | Il valore del denominatore. |
| [!UICONTROL Numeratore] | `numerator` | [[!UICONTROL Quantità]](../data-types/quantity.md) | Il valore del numeratore. |

>[!NOTE]
>
> `denominator` e `numerator` hanno tipi di dati diversi a causa della specifica creata in base alla versione 5 di HL7 FHIR.

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/ratio.schema.json)
