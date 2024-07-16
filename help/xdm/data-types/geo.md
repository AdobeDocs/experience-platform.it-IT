---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati geografici
description: Scopri il tipo di dati Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 35%

---

# Tipo di dati [!UICONTROL Geo]

[!UICONTROL Geo] è un tipo di dati XDM standard che descrive l&#39;area geografica in cui è stato osservato un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive le coordinate geografiche di un luogo. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
| `city` | Stringa | Il nome della città. |
| `countryCode` | Stringa | Codice a due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> per il paese. |
| `dmaID` | Intero | L’area di mercato designata da Nielsen Media Research. |
| `msaID` | Intero | L’area statistica metropolitana degli Stati Uniti in cui è avvenuta l’osservazione. |
| `postalCode` | Stringa | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi sarà inclusa solo una parte del codice postale. |
| `stateProvince` | Stringa | La porzione di stato o provincia dell’osservazione. Il formato segue lo standard [ISO 3166-2 (paese e suddivisione)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
