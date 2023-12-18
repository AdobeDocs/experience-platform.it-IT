---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati indirizzo postale
description: Scopri il tipo di dati XDM dell’indirizzo postale.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# [!UICONTROL Indirizzo postale] tipo di dati

[!UICONTROL Indirizzo postale] è un tipo di dati XDM standard che descrive i dettagli di un indirizzo postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `city` | Il nome della città. |
| `country` | Il nome del territorio amministrato dal governo. Questo è un campo in formato libero che può contenere il nome del paese in qualsiasi lingua. |
| `countryCode` | I due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> codice del paese. |
| `createdByBatchID` | ID del file batch acquisito che ha creato il record indirizzo. |
| `dmaID` | L&#39;area di mercato designata da Nielsen Media Research. |
| `label` | Nome in formato libero per l&#39;indirizzo. |
| `lastVerifiedDate` | La data in cui è stato verificato l’ultima volta che l’indirizzo è ancora associato alla persona. |
| `modifiedByBatchID` | ID del file batch acquisito che ha modificato per ultimo il record. |
| `msaID` | L’area statistica metropolitana degli Stati Uniti in cui è avvenuta l’osservazione. |
| `postOfficeBox` | La casella postale dell’indirizzo. |
| `postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `primary` | Un valore booleano che indica se si tratta dell’indirizzo principale dell’individuo. Un profilo può averne solo uno `primary` in un determinato momento. |
| `region` | La regione, la contea o la parte di distretto dell’indirizzo. |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;ultimo utente che ha modificato il record. |
| `stateProvince` | La porzione di stato o provincia dell’osservazione. Il formato segue il [ISO 3166-2 (paese e suddivisione)](https://www.unece.org/cefact/locode/subdivisions.html) standard. |
| `status` | Indica se l’indirizzo può essere attualmente utilizzato. |
| `statusReason` | Una descrizione dell&#39;attuale `status`. |
| `street1` - `street4` | Questi quattro campi devono contenere informazioni di livello stradale primarie, numero di appartamento, numero civico e nome della strada. `street2` a `street4` sono facoltativi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
