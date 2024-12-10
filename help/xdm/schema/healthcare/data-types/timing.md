---
title: Tipo di dati temporali
description: Scopri il tipo di dati Timing Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Intervallo] tipo di dati

[!UICONTROL Timing] è un tipo di dati XDM (Experience Data Model) standard che descrive una pianificazione temporale che fornisce informazioni su un evento che può verificarsi più volte. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Timing della struttura del tipo di dati](../../../images/healthcare/data-types/timing.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Evento] | `event` | Array di DateTime | Quando si verifica l’evento. |
| [!UICONTROL Ripeti] | `repeat` | [[!UICONTROL Ripeti]](../data-types/repeat.md) | Informazioni su quando si verifica l’evento. |
| [!UICONTROL Codice] | `code` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il codice relativo all’evento. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
