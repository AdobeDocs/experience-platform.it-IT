---
title: Tipo di dati durata
description: Scopri il tipo di dati Durata Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL Durata] tipo di dati

[!UICONTROL Durata] è un tipo di dati XDM (Experience Data Model) standard che descrive un periodo di tempo. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati durata](../../images/data-types/healthcare/duration.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | Stringa | Forma codificata dell’unità di tempo. |
| [!UICONTROL Sistema] | `system` | Stringa | Sistema che descrive l’unità codificata, rappresentata come URI. |
| [!UICONTROL Unità] | `unit` | Stringa | L’unità di tempo rappresentata in millisecondi, secondi, minuti, ore, giorni, settimane, mesi o anni. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `ms` (millisecondi) </li> <li> `s` (secondi) </li> <li> `min` (minuti) </li> <li> `h` (ore) </li>  <li> `d` (giorni) </li> <li> `wk` (settimane) </li> <li> `mo` (mesi) </li> <li> `a` (anni) </li> |
| [!UICONTROL Valore] | `value` | Doppio | Il valore numerico per l’unità di tempo. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)
