---
title: Tipo di dati identificatore
description: Scopri il tipo di dati Identifier Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# Tipo di dati [!UICONTROL Identificatore]

[!UICONTROL Identificatore] è un tipo di dati XDM (Experience Data Model) standard che fornisce un identificatore destinato al calcolo. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati dell&#39;identificatore](../../../images/healthcare/data-types/identifier.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Il periodo di tempo in cui l’ID è o era valido per l’uso. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Descrizione dell&#39;identificatore. |
| [!UICONTROL Assegnatario] | `assigner` | Stringa | Organizzazione che ha emesso l’ID. |
| [!UICONTROL Sistema] | `system` | Stringa | Lo spazio dei nomi per il valore dell’identificatore, rappresentato come URI. |
| [!UICONTROL Usa] | `use` | Stringa | L’utilizzo dell’identificatore. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL Valore] | `value` | Stringa | Il valore univoco dell’ID. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)
