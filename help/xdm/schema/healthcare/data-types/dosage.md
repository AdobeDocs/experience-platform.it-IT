---
title: Tipo Di Dati Di Dosaggio
description: Scopri il tipo di dati Dosage Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 56eda38b-a7f7-40da-af08-73cfe9db0c7e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Dosaggio]

[!UICONTROL Dosaggio] è un tipo di dati Experience Data Model (XDM) standard che descrive come il farmaco è/è stato assunto o deve essere assunto. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del dosaggio](../../../images/healthcare/data-types/dosage/dosage.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Istruzioni aggiuntive] | `additionalInstruction` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Istruzioni o avvertenze supplementari per il paziente. |
| [!UICONTROL Come Necessario Per] | `asNeededFor` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Descrive per quale problema il farmaco deve essere assunto secondo necessità. |
| [!UICONTROL Dose E Frequenza] | `doseAndRate` | Array di oggetti | La quantità di medicinale da somministrare o la quantità tipica da somministrare. Per ulteriori informazioni, consulta la [sezione seguente](#dose-and-rate) |
| [!UICONTROL Dose Massima Per Amministrazione] | `maxDosePerAdministration` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | Limite superiore del medicinale per somministrazione. |
| [!UICONTROL Dose Massima Per Vita] | `maxDosePerLifetime` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | Limite superiore del medicinale per tutta la vita del paziente. |
| [!UICONTROL Dose Massima Per Periodo] | `maxDosePerPeriod` | Array di [[!UICONTROL Rapporto]](../data-types/ratio.md) | Limite superiore del medicinale per unità di tempo. |
| [!UICONTROL Metodo] | `method` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La tecnica di somministrazione del farmaco. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Come il farmaco dovrebbe entrare nel corpo. |
| [!UICONTROL Sito corpo] | `site` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il sito corporeo in cui somministrare il farmaco. |
| [!UICONTROL Intervallo] | `timing` | [[!UICONTROL Intervallo]](../data-types/timing.md) | Quando somministrare il medicinale. |
| [!UICONTROL Secondo Necessità] | `asNeeded` | Booleano | Un indicatore per stabilire se il medicinale deve essere assunto secondo necessità. |
| [!UICONTROL Istruzioni per il paziente] | `patientInstruction` | Stringa | Istruzioni da comprendere per il paziente o il consumatore. |
| [!UICONTROL Sequenza] | `Integer` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | L’ordine delle istruzioni per il dosaggio. |
| [!UICONTROL Testo] | `text` | Stringa | Pianificare istruzioni testuali sul dosaggio. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura dose e velocità](../../../images/healthcare/data-types/dosage/dose-and-rate.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Quantità Di Dose] | `doseQuantity` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | La quantità di medicinale per dose. |
| [!UICONTROL Intervallo di dose] | `doseRange` | [[!UICONTROL Range]](../data-types/range.md) | La quantità di medicinale per dose. |
| [!UICONTROL Quantità tariffa] | `rateQuantity` | [[!UICONTROL Quantità semplice]](../data-types/simple-quantity.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Intervallo di frequenza] | `rateRange` | [[!UICONTROL Range]](../data-types/range.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Rapporto di frequenza] | `rateRatio` | [[!UICONTROL Rapporto]](../data-types/ratio.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il tipo di dose o la velocità specificata. |
