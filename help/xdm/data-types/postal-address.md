---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;address;xdm:address;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati indirizzo postale
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo postale.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# [!UICONTROL Postal address] tipo di dati

[!UICONTROL Postal address] è un tipo di dati XDM standard che descrive i dettagli di un indirizzo postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `city` | Il nome della città. |
| `country` | Nome del territorio amministrato dal governo. Si tratta di un campo a forma libera che può avere il nome del paese in qualsiasi lingua. |
| `countryCode` | Codice <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> a due caratteri per il paese. |
| `createdByBatchID` | ID del file batch assimilato che ha creato il record di indirizzo. |
| `dmaID` | Nielsen Media Research ha designato un&#39;area di mercato. |
| `label` | Un nome a forma libera per l&#39;indirizzo. |
| `lastVerifiedDate` | Data in cui l’indirizzo è stato verificato per l’ultima volta come ancora associato alla persona. |
| `modifiedByBatchID` | ID del file batch assimilato che ha modificato per ultimo il record. |
| `msaID` | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postOfficeBox` | La casella postale dell&#39;indirizzo. |
| `postalCode` | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `primary` | Un valore booleano che indica se si tratta dell&#39;indirizzo principale dell&#39;individuo. Un profilo può avere un solo `primary` indirizzo alla volta. |
| `region` | La regione, la contea o la parte del distretto dell&#39;indirizzo. |
| `repositoryCreatedBy` | L&#39;ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | L&#39;ID dell&#39;ultimo utente che ha modificato il record. |
| `stateProvince` | La parte dell&#39;osservazione relativa allo stato o alla provincia. Il formato è conforme allo standard [ISO 3166-2 (paese e suddivisione)](http://www.unece.org/cefact/locode/subdivisions.html) . |
| `status` | Indica se l&#39;indirizzo può essere utilizzato al momento. |
| `statusReason` | Una descrizione della corrente `status`. |
| `street1` - `street4` | Questi quattro campi sono destinati a contenere informazioni primarie a livello di strada, numero di appartamento, numero di strada e nome della strada. `street2` to `street4` sono facoltativi. |

Per ulteriori dettagli sul tipo di dati dell&#39;indirizzo postale, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)