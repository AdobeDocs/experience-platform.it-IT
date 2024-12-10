---
title: Tipo di dati disponibilità
description: Scopri il tipo di dati Experience Data Model (XDM) per la disponibilità.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 18c0b767-adf0-480e-9cf2-63e21d05b362
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 9%

---

# Tipo di dati [!UICONTROL Disponibilità]

[!UICONTROL Disponibilità] è un tipo di dati XDM (Experience Data Model) standard che descrive i dati di disponibilità per un elemento. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati di disponibilità](../../../images/healthcare/data-types/availability/availability.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Tempo disponibile] | `availableTime` | Array di oggetti | Gli orari in cui l&#39;elemento è disponibile. Per ulteriori informazioni, consulta la [sezione seguente](#available-time). |
| [!UICONTROL Ora non disponibile] | `notAvailableTime` | Stringa | Gli orari in cui l’elemento non è disponibile, con un motivo fornito. Per ulteriori informazioni, consulta la [sezione seguente](#not-available-time). |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/availability.schema.json)

## `availableTime` {#available-time}

`availableTime` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura del tempo disponibile](../../../images/healthcare/data-types/availability/available-time.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Tutto il giorno] | `allDay` | Booleano | Valore booleano che indica se l’elemento è sempre disponibile. |
| [!UICONTROL Ora di fine disponibile] | `availableEndTime` | Stringa | L&#39;ora del giorno in cui l&#39;elemento smette di essere disponibile. Questo viene ignorato se `allDay` è `true`. |
| [!UICONTROL Ora di inizio disponibile] | `availableStartTime` | Stringa | L&#39;ora del giorno in cui l&#39;elemento inizia a essere disponibile. Questo viene ignorato se `allDay` è `true`. |
| [!UICONTROL Giorni Della Settimana] | `daysOfWeek` | Array di stringhe | Matrice di stringhe che indica i giorni disponibili. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |

## `notAvailableTime` {#not-available-time}

`notAvailableTime` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura del tempo non disponibile](../../../images/healthcare/data-types/availability/not-available-time.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Durante] | `during` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di tempo in cui l&#39;elemento non è più disponibile. |
| [!UICONTROL Descrizione] | `description` | Stringa | Motivo per cui l&#39;elemento non è disponibile. |
