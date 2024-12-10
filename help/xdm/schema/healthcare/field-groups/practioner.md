---
title: Gruppo di campi schema professionista
description: Scopri il gruppo di campi Schema praticante.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 7%

---

# Gruppo di campi schema [!UICONTROL Professionista]

[!UICONTROL Professionista] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e la [[!DNL Provider class]](../../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcarePractioner` contenente informazioni su una persona che è direttamente o indirettamente coinvolta nella fornitura di servizi sanitari o servizi correlati.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Indirizzo] | `address` | Array di [[!UICONTROL Indirizzo]](../data-types/address.md) | Indirizzo/i del professionista che si trova al di fuori del luogo di lavoro, ad esempio l&#39;indirizzo dell&#39;abitazione. |
| [!UICONTROL Comunicazione] | `communication` | Array di oggetti | Una lingua che può essere utilizzata per comunicare con il professionista. Per ulteriori informazioni, consulta la [sezione seguente](#communication) |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Un identificatore che si applica a questa persona in questo ruolo. |
| [!UICONTROL Nome] | `name` | Array di [[!UICONTROL Nome umano]](../data-types/human-name.md) | Nome/i associato/i al professionista. |
| [!UICONTROL Qualifica] | `qualification` | Array di oggetti | Le qualifiche ufficiali, le certificazioni, gli accreditamenti, la formazione, le licenze o simili che autorizzano o altrimenti si riferiscono alla prestazione di assistenza da parte del professionista. Per ulteriori informazioni, consulta la [sezione seguente](#qualification). |
| [!UICONTROL Dettagli contatto] | `telecom` | Array di [[!UICONTROL punto di contatto]](../data-types/contact-point.md) | I recapiti del professionista. |
| [!UICONTROL Attivo] | `active` | Booleano | Indica se il record dei professionisti è in uso attivo. |
| [!UICONTROL Data di nascita] | `birthDate` | Data | La data di nascita del professionista. |
| [!UICONTROL Indicatore defunto] | `deceasedBoolean` | Booleano | Indica se il professionista è deceduto. |
| [!UICONTROL Data/ora decesso] | `deceasedDateTime` | Data e ora | La data e l’ora della morte del medico. |
| [!UICONTROL Genere] | `gender` | Stringa | L’identità di genere della persona. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura di comunicazione](../../../images/healthcare/field-groups/practitioner/communication.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Lingua] | `language` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il linguaggio che può essere utilizzato per comunicare con la persona sulla sua salute. |
| [!UICONTROL Lingua Preferita] | `preferred` | Booleano | Indica se la lingua è la loro lingua preferita o meno. |

## `qualification` {#qualification}

`qualification` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura delle qualifiche](../../../images/healthcare/field-groups/practitioner/qualification.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La rappresentazione codificata della qualifica. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Un identificatore per la qualifica. |
| [!UICONTROL Emittente] | `issuer` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L’organizzazione che regola e rilascia la qualifica. |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di validità della qualifica. |
