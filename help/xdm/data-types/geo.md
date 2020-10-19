---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati geografico
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati Geo XDM.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---


# [!UICONTROL Geo] tipo di dati

[!UICONTROL Geo] è un tipo di dati XDM standard che descrive l&#39;area geografica in cui è stato osservato un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive le coordinate geografiche di un luogo. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
| `city` | Stringa | Il nome della città. |
| `countryCode` | Stringa | Codice <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> a due caratteri per il paese. |
| `dmaID` | Intero | Nielsen Media Research ha designato un&#39;area di mercato. |
| `msaID` | Intero | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postalCode` | Stringa | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `stateProvince` | Stringa | La parte dell&#39;osservazione relativa allo stato o alla provincia. Il formato è conforme allo standard [ISO 3166-2 (paese e suddivisione)](http://www.unece.org/cefact/locode/subdivisions.html) . |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)