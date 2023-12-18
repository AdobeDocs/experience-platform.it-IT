---
title: Tipo di dati indirizzo postale
description: Scopri il tipo di dati XDM (Postal Address Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 8%

---

# [!UICONTROL Indirizzo postale] tipo di dati

[!UICONTROL Indirizzo postale] è un tipo di dati Experience Data Model (XDM) standard che fornisce dettagli sull’indirizzo.

![Un diagramma del [!UICONTROL Indirizzo postale] tipo di dati.](../images/data-types/postal-address.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principale] | `primary` | booleano | Indicatore dell’indirizzo primario. Un profilo può averne solo uno `primary` in un determinato momento. |
| [!UICONTROL Etichetta] | `label` | string | Nome in formato libero dell’indirizzo. |
| [!UICONTROL Strada 1] | `street1` | string | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| [!UICONTROL Strada 2] | `street2` | string | Seconda riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Strada 3] | `street3` | string | Terza riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Strada 4] | `street4` | string | Quarta riga facoltativa sulle informazioni stradali. |
| [!UICONTROL Regione] | `region` | string | La regione, la contea o la parte di distretto dell’indirizzo. |
| [!UICONTROL Casella postale] | `postOfficeBox` | string | Casella postale dell’indirizzo. |
| [!UICONTROL Paese] | `country` | string | Il nome del territorio amministrato dal governo. Diverso da ``countryCode``, questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| [!UICONTROL Stato] | `state` | string | Il nome dello Stato. Questo è un campo in formato libero. |
| [!UICONTROL Stato] | `status` | string | Un’indicazione relativa alla possibilità di utilizzare l’indirizzo. |
| [!UICONTROL Motivo dello stato] | `statusReason` | string | Descrizione dello stato corrente. |
| [!UICONTROL Data ultima verifica] | `lastVerifiedDate` | string | La data in cui è stato verificato l’ultima volta che l’indirizzo è ancora associato alla persona. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta [schema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) sull’archivio XDM pubblico:
