---
keywords: Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;schemi;schemi;geo;geo;geo shape;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati a forma di geo
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM della forma Geo.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# [!UICONTROL Geo Shape] tipo di dati

[!UICONTROL Geo Shape] è un tipo di dati XDM standard che descrive la forma di un’area geografica. Questo tipo di dati si basa sulle specifiche pubbliche documentate su [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.box` | Array di [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive un&#39;area geografica delimitata da un rettangolo formato da due coordinate. La prima coordinata è l&#39;angolo inferiore del rettangolo e la seconda è l&#39;angolo superiore. |
| `_schema.circle` | Array di [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive un&#39;area circolare con un raggio specifico centrato su una coordinata geografica. |
| `_schema.polygon` | [[!UICONTROL Geo Circle]](./geo-circle.md) | Una serie di quattro o più coordinate in cui la prima e la finale coordinate sono identiche. |
| `_schema.description` | Stringa | Descrizione della definizione della forma. |
| `_schema.elevation` | Doppio | L&#39;elevazione specifica o minima della forma. Questo valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `ceiling`, questa proprietà può essere utilizzata per esprimere un riquadro di delimitazione tridimensionale per una posizione. |
| `_id` | Stringa | Identificatore univoco generato dal sistema per la forma. |
| `ceiling` | Doppio | L&#39;elevazione massima della forma. Questa proprietà è valida solo se utilizzata in combinazione con `elevation`. Il valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `elevation`, questa proprietà può essere utilizzata per esprimere un riquadro di delimitazione tridimensionale per una posizione. |
