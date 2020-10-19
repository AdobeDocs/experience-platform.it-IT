---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;poi details;point of interest;point of interest details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati dei dettagli del punto di interesse
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Dettagli punto di interesse.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 4%

---


# [!UICONTROL Point of interest details] tipo di dati

[!UICONTROL Point of interest details] è un tipo di dati XDM standard che descrive i dati relativi alla posizione geografica in cui è stato osservato un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descrive i dettagli beacon attivi per l’interazione POI. |
| `geoInteractionDetails` | [[!UICONTROL Geo interaction details]](./geo-interaction-details.md) | Descrive i dettagli geografici attivi per l’interazione POI. |
| `category` | Stringa | Categoria generale assegnata dall’amministratore delle definizioni dei punti di interesse (POI) per l’organizzazione dei punti di interesse. |
| `distanceToPOICenter` | Doppio | La distanza stimata dal centro POI in metri. |
| `locatingType` | Stringa | Meccanismo utilizzato per determinare la posizione. I valori accettati includono: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Stringa | Un nome dato al POI. |
| `poiID` | Stringa | Identificatore univoco del POI. |
| `type` | Stringa | Il tipo generale di POI che utilizza uno schema di digitazione selezionato dall’amministratore delle definizioni dei POI. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)