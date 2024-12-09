---
title: Ripeti tipo di dati
description: Scopri il tipo di dati Repeat Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL Ripeti] tipo di dati

[!UICONTROL Repeat] è un tipo di dati XDM (Experience Data Model) standard che fornisce un set di regole che descrivono quando un evento è pianificato. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Ripeti struttura tipo di dati](../../images/data-types/healthcare/reference.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Periodo associato] | `boundsPeriod` | [[!UICONTROL Periodo]](../healthcare/period.md) | Gli orari di inizio e fine. |
| [!UICONTROL Intervallo associato] | `boundsRange` | [[!UICONTROL Range]](../healthcare/range.md) | Il limite dell’intervallo. |
| [!UICONTROL Durata associata] | `boundsDuration` | [[!UICONTROL Durata]](../healthcare/duration.md) | Il limite di durata. |
| [!UICONTROL Conteggio] | `count` | Intero | Il numero di volte da ripetere, con un valore minimo di `0`. |
| [!UICONTROL Numero massimo] | `countMax` | Intero | Numero massimo di ripetizioni, con valore minimo di `0`. |
| [!UICONTROL Giorno Della Settimana] | `dayOfWeek` | Array di stringhe | Matrice di stringhe che indica i giorni disponibili. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL Durata] | `duration` | Doppio | La durata. |
| [!UICONTROL Durata massima] | `durationMax` | Doppio | La durata massima. |
| [!UICONTROL Unità di Durata] | `durationUnit` | Stringa | L’unità di durata. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `s` (secondi) </li> <li> `min` (minuti) </li> <li> `h` (ogni ora) </li> <li> `d` (giornaliero) </li>  <li> `wk` (settimanale) </li> <li> `mo` (mensile) </li> <li> `a` (annuale)</li> |
| [!UICONTROL Frequenza] | `frequency` | Doppio | Il numero di ripetizioni che devono verificarsi in un periodo, con un valore minimo di `0`. |
| [!UICONTROL Frequenza massima] | `frequencyMax` | Doppio | Il numero massimo di ripetizioni che devono verificarsi con un punto, con un valore minimo di `0`. |
| [!UICONTROL Offset] | `offset` | Intero | I minuti fino all’evento (prima o dopo). |
| [!UICONTROL Periodo] | `period` | Doppio | La durata della frequenza. |
| [!UICONTROL Periodo massimo] | `periodMax` | Doppio | Limite superiore del periodo. |
| [!UICONTROL Unità periodo] | `periodUnit` | Stringa | Unità di tempo. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `s` (secondi) </li> <li> `min` (minuti) </li> <li> `h` (ogni ora) </li> <li> `d` (giornaliero) </li>  <li> `wk` (settimanale) </li> <li> `mo` (mensile) </li> <li> `a` (annuale)</li> |
| [!UICONTROL Ora Del Giorno] | `timeOfDay` | Array di stringhe | L’ora del giorno in cui si verifica l’azione. |
| [!UICONTROL When] | `when` | Array di stringhe | Il codice per il periodo di tempo dell’azione. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)
