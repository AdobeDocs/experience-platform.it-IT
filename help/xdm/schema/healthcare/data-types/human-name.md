---
title: Tipo di dati nome umano
description: Scopri il tipo di dati Human Name Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Nome umano]

[!UICONTROL Nome umano] è un tipo di dati XDM (Experience Data Model) standard che fornisce informazioni sul nome di un&#39;entità umana o di un&#39;altra entità vivente. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura tipo dati Nome umano](../../../images/healthcare/data-types/human-name.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Il periodo di tempo in cui il nome è o era in uso. |
| [!UICONTROL Famiglia] | `family` | Stringa | La famiglia o il cognome. |
| [!UICONTROL Dato] | `given` | Array di stringhe | Il nome specificato, compresi eventuali nomi intermedi. |
| [!UICONTROL Prefisso] | `prefix` | Array di stringhe | Qualsiasi parte del nome prima del nome o del nome. |
| [!UICONTROL Suffisso] | `suffix` | Array di stringhe | Qualsiasi parte del nome dopo la famiglia o il cognome. |
| [!UICONTROL Testo] | `text` | Stringa | Rappresentazione in testo normale del nome completo. |
| [!UICONTROL Usa] | `use` | Stringa | Uso del nome. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)
