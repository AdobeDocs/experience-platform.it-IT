---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati geo
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL Geo] tipo di dati

[!UICONTROL Geo] è un tipo di dati XDM standard che descrive l’area geografica in cui è stato osservato un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive le coordinate geografiche di un luogo. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
| `city` | Stringa | Il nome della città. |
| `countryCode` | Stringa | I due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> codice del paese. |
| `dmaID` | Intero | La ricerca sui media Nielsen ha designato un&#39;area di mercato. |
| `msaID` | Intero | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postalCode` | Stringa | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `stateProvince` | Stringa | La parte dello stato o della provincia dell&#39;osservazione. Il formato segue le [ISO 3166-2 (paese e sottodivisione)](https://www.unece.org/cefact/locode/subdivisions.html) standard. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
