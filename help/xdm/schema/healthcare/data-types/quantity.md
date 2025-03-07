---
title: Tipo di dati quantità
description: Scopri il tipo di dati Quantity Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 881fe8a4-0253-4b75-9833-b97bb50cc87e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 11%

---

# Tipo di dati [!UICONTROL Quantità]

[!UICONTROL Quantità] è un tipo di dati XDM (Experience Data Model) standard che fornisce una quantità misurata o misurabile. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura tipo dati quantità](../../../images/healthcare/data-types/quantity.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | Stringa | La forma codificata dell’unità. |
| [!UICONTROL Comparatore] | `comparator` | Stringa | Operatore di confronto. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `<` </li> <li> `<=` </li> <li> `>=` </li> <li> `>`</li> <li> `ad`</li> |
| [!UICONTROL Sistema] | `system` | Stringa | Il sistema che definisce il modulo di unità codificata, rappresentato come URI. |
| [!UICONTROL Unità] | `unit` | Stringa | La rappresentazione dell’unità. |
| [!UICONTROL Valore] | `value` | Doppio | Il valore numerico. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/quantity.schema.json)
