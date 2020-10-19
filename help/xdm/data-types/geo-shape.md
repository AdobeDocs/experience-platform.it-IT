---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;geo shape;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati Geo Shape
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM della forma geografica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---


# [!UICONTROL Geo Shape] tipo di dati

[!UICONTROL Geo Shape] è un tipo di dati XDM standard che descrive la forma di un&#39;area geografica. Questo tipo di dati si basa sulle specifiche pubbliche documentate in [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.box` | Matrice di [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive un&#39;area geografica racchiusa da un rettangolo formato da due coordinate. La prima coordinata è l’angolo inferiore del rettangolo e la seconda è l’angolo superiore. |
| `_schema.circle` | Matrice di [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive un&#39;area circolare con un raggio specifico centrato su una coordinata geografica. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Una serie di quattro o più coordinate in cui la prima e l&#39;ultima coordinate sono identiche. |
| `_schema.description` | Stringa | Una descrizione della definizione della forma. |
| `_schema.elevation` | Doppio | L&#39;elevazione specifica o minima della forma. Questo valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `ceiling`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
| `_id` | Stringa | Identificatore univoco generato dal sistema per la forma. |
| `ceiling` | Doppio | L&#39;elevazione massima della forma. Questa proprietà è valida solo se utilizzata in combinazione con `elevation`. Il valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `elevation`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
