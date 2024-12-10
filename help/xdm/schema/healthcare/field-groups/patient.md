---
title: Gruppo di campi schema paziente
description: Scopri il gruppo di campi Schema paziente.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: eba7deb3-4785-4d05-86ef-0f6691fcd2c5
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 7%

---

# [!UICONTROL Paziente] gruppo di campi dello schema

[!UICONTROL Paziente] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md). Fornisce un singolo campo di tipo oggetto `healthcarePatient` che acquisisce i dati demografici e altri dettagli amministrativi su un individuo o un animale che riceve cure o altri servizi sanitari.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/patient/patient.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Indirizzo] | `address` | Array di [[!UICONTROL Indirizzo]](../data-types/address.md) | Informazioni sull’indirizzo del paziente. |
| [!UICONTROL Comunicazione] | `communication` | Array di oggetti | Un linguaggio che può essere usato per comunicare con il paziente circa la sua salute. Per ulteriori informazioni, consulta la [sezione seguente](#communication). |
| [!UICONTROL Contatti paziente] | `contact` | Array di oggetti | Gruppo di contatto di un paziente, ad esempio un tutore, un partner o un amico. Per ulteriori informazioni, consulta la [sezione seguente](#contact). |
| [!UICONTROL Professionista generico] | `generalPractioner` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Il fornitore di cure primarie del paziente. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Un identificatore del paziente. |
| [!UICONTROL Dettagli collegamento paziente] | `link` | Array di oggetti | Collegamento alla risorsa di un paziente o di una persona correlata che riguarda la stessa persona. Per ulteriori informazioni, consulta la [sezione seguente](#link). |
| [!UICONTROL Gestione dell&#39;organizzazione] | `managingOrganization` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L&#39;organizzazione della custodia dei dati del paziente. |
| [!UICONTROL Stato civile] | `maritalStatus` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Lo stato civile del paziente. |
| [!UICONTROL Nome] | `name` | Array di [[!UICONTROL Nome umano]](../data-types/human-name.md) | Il nome associato al paziente. |
| [!UICONTROL Dettagli contatto] | `telecom` | Array di [[!UICONTROL punto di contatto]](../data-types/contact-point.md) | Un recapito di contatto, ad esempio un numero di telefono o un indirizzo e-mail, tramite il quale il paziente può essere contattato. |
| [!UICONTROL È Attivo] | `active` | Booleano | Indica se la cartella clinica del paziente è in uso attivo. |
| [!UICONTROL Data di nascita] | `birthDate` | Data | La data di nascita del paziente. |
| [!UICONTROL Indicatore defunto] | `deceasedBoolean` | Booleano | Indica se il paziente è deceduto o meno. |
| [!UICONTROL Data/ora decesso] | `deceasedDateTime` | Data e ora | La data e l’ora del decesso del paziente. |
| [!UICONTROL Genere] | `gender` | Stringa | L’identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |
| [!UICONTROL Fa Parte Di Una Nascita Multipla] | `multipleBirthBoolean` | Booleano | Indica se il paziente fa parte di un parto multiplo. |
| [!UICONTROL Numero di nascita] | `multipleBirthInteger` | Intero | Il numero di nascita nella sequenza. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.schema.json)

## `communication` {#communication}

`communication` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura di comunicazione](../../../images/healthcare/field-groups/patient/communication.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Lingua] | `language` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il linguaggio che può essere utilizzato per comunicare con la persona sulla sua salute. |
| [!UICONTROL Lingua Preferita] | `preferred` | Booleano | Indica se la lingua è la loro lingua preferita o meno. |

## `contact` {#contact}

`contact` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura contatti](../../../images/healthcare/field-groups/patient/contact.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Indirizzo contatto] | `address` | [[!UICONTROL Indirizzo]](../data-types/address.md) | Indirizzo della persona di contatto. |
| [!UICONTROL Nome contatto] | `name` | [[!UICONTROL Nome umano]](../data-types/human-name.md) | Il nome della persona di contatto. |
| [!UICONTROL Contatta organizzazione] | `organization` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Organizzazione associata alla persona di contatto. |
| [!UICONTROL Periodo di contatto] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Il periodo di tempo in cui il contatto era o è in uso. |
| [!UICONTROL Relazione&#39;] | `relationship` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il rapporto tra il paziente e la persona di contatto. |
| [!UICONTROL Dettagli contatto] | `telecom` | Array di oggetti | I recapiti della persona di contatto. Per ulteriori informazioni, consulta la [sezione seguente](#telecom). |
| [!UICONTROL Genere] | `gender` | Stringa | L’identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

### `telecom` {#telecom}

`telecom` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura telecom](../../../images/healthcare/field-groups/patient/telecom.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Punto di contatto] | `contactPoint` | [[!UICONTROL Punto di contatto]](../data-types/contact-point.md) | I dettagli di contatto della persona. |

## `link` {#link}

`link` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura collegamento](../../../images/healthcare/field-groups/patient/link.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Altre] | `other` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Collegamento alla risorsa di un paziente o di una persona correlata che riguarda la stessa persona. |
| [!UICONTROL Tipo] | `type` | Stringa | Il tipo di collegamento tra le due risorse del paziente. |
