---
title: Tipo di dati temporali
description: Scopri il tipo di dati Timing Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 0640d0c2daab67ad7a77d3265ccae45851ba45b8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL Intervallo] tipo di dati

[!UICONTROL Timing] è un tipo di dati XDM (Experience Data Model) standard che descrive una pianificazione temporale che fornisce informazioni su un evento che può verificarsi più volte. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Timing della struttura del tipo di dati](../../images/data-types/healthcare/timing.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Evento] | `event` | Array di DateTime | Quando si verifica l’evento. |
| [!UICONTROL Ripeti] | `repeat` | [[!UICONTROL Ripeti]](../healthcare/repeat.md) | Informazioni su quando si verifica l’evento. |
| [!UICONTROL Codice] | `code` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Il codice relativo all’evento. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)
