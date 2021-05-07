---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati geo
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---

# [!UICONTROL Geo] tipo di dati

[!UICONTROL Geo] è un tipo di dati XDM standard che descrive l’area geografica in cui è stato osservato un evento.

<img src="../images/data-types/geo.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive le coordinate geografiche di un luogo. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
| `city` | Stringa | Il nome della città. |
| `countryCode` | Stringa | Il codice a due caratteri <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> per il paese. |
| `dmaID` | Intero | La ricerca sui media Nielsen ha designato un&#39;area di mercato. |
| `msaID` | Intero | L&#39;area statistica metropolitana negli Stati Uniti dove si è verificata l&#39;osservazione. |
| `postalCode` | Stringa | Codice postale della posizione. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi ciò conterrà solo una parte del codice postale. |
| `stateProvince` | Stringa | La parte dello stato o della provincia dell&#39;osservazione. Il formato è conforme allo standard [ISO 3166-2 (paese e suddivisione)](http://www.unece.org/cefact/locode/subdivisions.html). |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)
