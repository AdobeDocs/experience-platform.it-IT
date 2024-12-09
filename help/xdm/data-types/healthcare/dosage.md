---
title: Tipo Di Dati Di Dosaggio
description: Scopri il tipo di dati Dosage Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Dosaggio]

[!UICONTROL Dosaggio] è un tipo di dati Experience Data Model (XDM) standard che descrive come il farmaco è/è stato assunto o deve essere assunto. Questo tipo di dati viene creato in base alle specifiche HL7 FHIR Release 5.

![Struttura del tipo di dati del dosaggio](../../images/data-types/healthcare/dosage/dosage.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Istruzioni aggiuntive] | `additionalInstruction` | Array di [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Istruzioni o avvertenze supplementari per il paziente. |
| [!UICONTROL Come Necessario Per] | `asNeededFor` | Array di [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Descrive per quale problema il farmaco deve essere assunto secondo necessità. |
| [!UICONTROL Dose E Frequenza] | `doseAndRate` | Array di oggetti | La quantità di medicinale da somministrare o la quantità tipica da somministrare. Per ulteriori informazioni, consulta la [sezione seguente](#dose-and-rate) |
| [!UICONTROL Dose Massima Per Amministrazione] | `maxDosePerAdministration` | [[!UICONTROL Quantità semplice]](../healthcare/simple-quantity.md) | Limite superiore del medicinale per somministrazione. |
| [!UICONTROL Dose Massima Per Vita] | `maxDosePerLifetime` | [[!UICONTROL Quantità semplice]](../healthcare/simple-quantity.md) | Limite superiore del medicinale per tutta la vita del paziente. |
| [!UICONTROL Dose Massima Per Periodo] | `maxDosePerPeriod` | Array di [[!UICONTROL Rapporto]](../healthcare/ratio.md) | Limite superiore del medicinale per unità di tempo. |
| [!UICONTROL Metodo] | `method` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | La tecnica di somministrazione del farmaco. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Come il farmaco dovrebbe entrare nel corpo. |
| [!UICONTROL Sito corpo] | `site` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Il sito corporeo in cui somministrare il farmaco. |
| [!UICONTROL Intervallo] | `timing` | [[!UICONTROL Intervallo]](../healthcare/timing.md) | Quando somministrare il medicinale. |
| [!UICONTROL Secondo Necessità] | `asNeeded` | Booleano | Un indicatore per stabilire se il medicinale deve essere assunto secondo necessità. |
| [!UICONTROL Istruzioni per il paziente] | `patientInstruction` | Stringa | Istruzioni da comprendere per il paziente o il consumatore. |
| [!UICONTROL Sequenza] | `Integer` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | L’ordine delle istruzioni per il dosaggio. |
| [!UICONTROL Testo] | `text` | Stringa | Pianificare istruzioni testuali sul dosaggio. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/dosage.schema.json)

## `doseAndRate` {#dose-and-rate}

`doseAndRate` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura dose e velocità](../../images/data-types/healthcare/dosage/dose-and-rate.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Quantità Di Dose] | `doseQuantity` | [[!UICONTROL Quantità semplice]](../healthcare/simple-quantity.md) | La quantità di medicinale per dose. |
| [!UICONTROL Intervallo di dose] | `doseRange` | [[!UICONTROL Range]](../healthcare/range.md) | La quantità di medicinale per dose. |
| [!UICONTROL Quantità tariffa] | `rateQuantity` | [[!UICONTROL Quantità semplice]](../healthcare/simple-quantity.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Intervallo di frequenza] | `rateRange` | [[!UICONTROL Range]](../healthcare/range.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Rapporto di frequenza] | `rateRatio` | [[!UICONTROL Rapporto]](../healthcare/ratio.md) | La quantità di medicinale per unità di tempo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../healthcare/codeable-concept.md) | Il tipo di dose o la velocità specificata. |
