---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati indirizzo postale
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo postale.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Tipo di dati ] indirizzo postale

[!UICONTROL L’] indirizzo postale è un tipo di dati XDM standard che descrive i dettagli di un indirizzo postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `city` | Il nome della città. |
| `country` | Nome del territorio amministrato dal governo. Questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `countryCode` | Il codice a due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> per il paese. |
| `createdByBatchID` | ID del file batch acquisito che ha creato il record di indirizzi. |
| `dmaID` | La ricerca sui media Nielsen ha designato un&#39;area di mercato. |
| `label` | Nome a forma libera per l’indirizzo. |
| `lastVerifiedDate` | Data dell&#39;ultima verifica dell&#39;indirizzo associata alla persona. |
| `modifiedByBatchID` | ID del file batch acquisito che ha modificato per ultimo il record. |
| `msaID` | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postOfficeBox` | La casella postale dell&#39;indirizzo. |
| `postalCode` | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `primary` | Un valore booleano che indica se si tratta dell&#39;indirizzo principale dell&#39;individuo. Un profilo può avere un solo indirizzo `primary` in un dato momento. |
| `region` | La parte dell&#39;indirizzo relativa alla regione, alla provincia o al distretto. |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |
| `stateProvince` | La parte dello stato o della provincia dell&#39;osservazione. Il formato è conforme allo standard [ISO 3166-2 (paese e suddivisione)](http://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indica se l’indirizzo può essere attualmente utilizzato. |
| `statusReason` | Una descrizione del `status` corrente. |
| `street1` - `street4` | Questi quattro campi devono contenere informazioni primarie a livello di strada, numero di appartamento, numero di strada e nome della strada. `street2` to  `street4` sono facoltativi. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
