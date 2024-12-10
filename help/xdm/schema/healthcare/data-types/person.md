---
title: Tipo di dati della persona
description: Scopri il tipo di dati Person Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: a19823f2-25d0-45cb-86f4-7816041b27f9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 7%

---

# Tipo di dati [!UICONTROL Persona]

[!UICONTROL Persona] è un tipo di dati XDM (Experience Data Model) standard che fornisce informazioni su un record persona generico. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura tipo di dati persona](../../../images/healthcare/data-types/person/person.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Indirizzo] | `address` | Array di [[!UICONTROL Indirizzo]](../data-types/address.md) | Uno o più indirizzi per la persona. |
| [!UICONTROL Comunicazione] | `communication` | Array di oggetti | Una lingua che può essere utilizzata per comunicare con la persona circa la sua salute. Per ulteriori informazioni, consulta la [sezione seguente](#communication). |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Un identificatore umano per questa persona. |
| [!UICONTROL Dettagli collegamento persona] | `link` | Array di oggetti | Collegamento a una risorsa che riguarda la stessa persona effettiva. Per ulteriori informazioni, consulta la [sezione seguente](#link). |
| [!UICONTROL Gestione dell&#39;organizzazione] | `managingOrganization` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Organizzazione che custodisce la cartella clinica del paziente. |
| [!UICONTROL Stato civile] | `maritalStatus` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Stato civile di una persona |
| [!UICONTROL Nome] | `name` | Array di [[!UICONTROL Nome umano]](../data-types/human-name.md) | Nomi associati a una persona. |
| [!UICONTROL Dettagli contatto] | `telecom` | Array di [[!UICONTROL punto di contatto]] | I recapiti tramite i quali la persona può essere contattata. |
| [!UICONTROL È Attivo] | `active` | Booleano | Indica se il record della persona è in uso attivo. |
| [!UICONTROL Data di nascita] | `birthDate` | Data | La data di nascita della persona. |
| [!UICONTROL Indicatore defunto] | `deceasedBoolean` | Booleano | Indica se la persona è deceduta o meno. |
| [!UICONTROL Data/ora decesso] | `deceasedDateTime` | Data e ora | La data e l’ora del decesso se la persona è deceduta. |
| [!UICONTROL Genere] | `gender` | Stringa | L’identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

## `communication` {#communication}

`communication` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura di comunicazione](../../../images/healthcare/data-types/person/communication.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Lingua] | `language` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il linguaggio che può essere utilizzato per comunicare con la persona sulla sua salute. |
| [!UICONTROL Lingua Preferita] | `preferred` | Booleano | Indica se la lingua è la loro lingua preferita o meno. |

## `link` {#link}

`link` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura collegamento](../../../images/healthcare/data-types/person/link.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Target] | `target` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Risorsa a cui è associata la persona effettiva. |
| [!UICONTROL Assurance] | `assurance` | Stringa | Livello di garanzia associato al collegamento. I valori di questa proprietà devono essere uguali a uno o più dei seguenti valori enum noti. <li> `level1` </li> <li> `level2` </li> <li> `level3` </li> <li> `level4` </li> |
