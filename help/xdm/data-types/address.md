---
title: Tipo di dati indirizzo postale
description: Scopri il tipo di dati XDM (Postal Address Experience Data Model).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 41%

---

# Tipo di dati [!UICONTROL Indirizzo postale]

[!UICONTROL Postal Address] è un tipo di dati XDM (Experience Data Model) standard che fornisce dettagli sull&#39;indirizzo.

![Diagramma del tipo di dati [!UICONTROL Indirizzo postale].](../images/data-types/postal-address.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principale] | `primary` | booleano | Indicatore dell’indirizzo primario. Un profilo può avere un solo indirizzo `primary` in un determinato momento. |
| [!UICONTROL Etichetta] | `label` | stringa | Nome in forma libera dell’indirizzo. |
| [!UICONTROL Via 1] | `street1` | stringa | Informazioni stradali primarie, numero di appartamento, numero civico e nome della via. |
| [!UICONTROL Via 2] | `street2` | stringa | Seconda riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Via 3] | `street3` | stringa | Terza riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Via 4] | `street4` | stringa | Quarta riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Area] | `region` | stringa | La regione, la contea o la parte di distretto dell’indirizzo. |
| [!UICONTROL Office Box di Post] | `postOfficeBox` | stringa | Casella postale dell’indirizzo. |
| [!UICONTROL Paese] | `country` | stringa | Il nome del territorio amministrato dal governo. A parte ``countryCode``, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| [!UICONTROL Stato] | `state` | stringa | Nome della Stato o della provincia. Campo a forma libera. |
| [!UICONTROL Stato] | `status` | stringa | Un’indicazione relativa alla possibilità di utilizzare l’indirizzo. |
| [!UICONTROL Motivo dello stato] | `statusReason` | stringa | Descrizione dello stato corrente. |
| [!UICONTROL Data ultima verifica] | `lastVerifiedDate` | stringa | La data in cui è stato verificato l’ultima volta che l’indirizzo è ancora associato alla persona. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, fai riferimento allo [schema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) nell&#39;archivio XDM pubblico:
