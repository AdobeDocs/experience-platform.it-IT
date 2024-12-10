---
title: Tipo di dati dell’indirizzo
description: Scopri il tipo di dati Address Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 9%

---

# Tipo di dati [!UICONTROL Indirizzo]

[!UICONTROL Indirizzo] è un tipo di dati XDM (Experience Data Model) standard che descrive un indirizzo espresso utilizzando convenzioni postali (anziché GPS o altri formati di definizione della posizione). Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati indirizzo](../../../images/healthcare/data-types/address.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di tempo in cui l’indirizzo era/è in uso. |
| [!UICONTROL Città] | `city` | Stringa | Nome della città. |
| [!UICONTROL Paese] | `country` | Stringa | Il codice del paese descritto nella norma internazionale ISO 3166. Il codice può essere alfa-2 o alfa-3. |
| [!UICONTROL Distretto] | `district` | Stringa | Il nome del distretto. |
| [!UICONTROL Riga] | `line` | Stringa | Il nome della via, il numero, la direzione, la casella postale o simili. |
| [!UICONTROL Codice Postale] | `postalCode` | Stringa | Il codice postale. |
| [!UICONTROL Stato] | `state` | Stringa | L’unità secondaria di un paese. Le abbreviazioni sono accettabili. |
| [!UICONTROL Testo] | `text` | Stringa | La rappresentazione testuale dell’indirizzo. |
| [!UICONTROL Tipo] | `type` | Stringa | Il tipo di indirizzo. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Usa] | `use` | Stringa | Scopo dell’indirizzo. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
