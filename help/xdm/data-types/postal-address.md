---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;indirizzo;xdm:address;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati indirizzo postale
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo postale.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Indirizzo postale] tipo di dati

[!UICONTROL Indirizzo postale] è un tipo di dati XDM standard che descrive i dettagli di un indirizzo postale.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `city` | Il nome della città. |
| `country` | Nome del territorio amministrato dal governo. Questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `countryCode` | I due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> codice del paese. |
| `createdByBatchID` | ID del file batch acquisito che ha creato il record di indirizzi. |
| `dmaID` | La ricerca sui media Nielsen ha designato un&#39;area di mercato. |
| `label` | Nome a forma libera per l’indirizzo. |
| `lastVerifiedDate` | Data dell&#39;ultima verifica dell&#39;indirizzo associata alla persona. |
| `modifiedByBatchID` | ID del file batch acquisito che ha modificato per ultimo il record. |
| `msaID` | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postOfficeBox` | La casella postale dell&#39;indirizzo. |
| `postalCode` | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `primary` | Un valore booleano che indica se si tratta dell&#39;indirizzo principale dell&#39;individuo. Un profilo può avere solo un `primary` indirizzo in un determinato momento. |
| `region` | La parte dell&#39;indirizzo relativa alla regione, alla provincia o al distretto. |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |
| `stateProvince` | La parte dello stato o della provincia dell&#39;osservazione. Il formato segue le [ISO 3166-2 (paese e sottodivisione)](https://www.unece.org/cefact/locode/subdivisions.html) standard. |
| `status` | Indica se l’indirizzo può essere attualmente utilizzato. |
| `statusReason` | Descrizione dell&#39;attuale `status`. |
| `street1` - `street4` | Questi quattro campi devono contenere informazioni primarie a livello di strada, numero di appartamento, numero di strada e nome della strada. `street2` a `street4` sono facoltativi. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati dell’indirizzo postale, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
