---
title: Tipo di dati di riferimento
description: Scopri il tipo di dati Reference Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---

# [!UICONTROL Riferimento] tipo di dati

[!UICONTROL Riferimento] è un tipo di dati XDM (Experience Data Model) standard che fornisce un riferimento da una risorsa all&#39;altra. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati di riferimento](../../../images/healthcare/data-types/reference.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Identificatore] | `identifier` | [[!UICONTROL Identificatore]](../data-types/identifier.md) | Il riferimento logico quando il riferimento letterale non è noto. |
| [!UICONTROL Visualizzazione] | `display` | Stringa | Testo alternativo per il riferimento. |
| [!UICONTROL Riferimento] | `reference` | Stringa | Riferimento letterale, URL relativo, URL interno o URL assoluto. |
| [!UICONTROL Tipo] | `type` | Stringa | Il tipo a cui si riferisce il riferimento, rappresentato come URI. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)
