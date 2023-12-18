---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;geo shape;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati forma geografica
description: Scopri il tipo di dati XDM Geo Shape.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 3%

---

# [!UICONTROL Forma di geotargeting] tipo di dati

[!UICONTROL Forma di geotargeting] è un tipo di dati XDM standard che descrive la forma di un’area geografica. Questo tipo di dati si basa sulla specifica pubblica documentata in [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.box` | Array di [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive un&#39;area geografica racchiusa da un rettangolo formato da due coordinate. La prima coordinata è l&#39;angolo inferiore del rettangolo e la seconda coordinata è l&#39;angolo superiore. |
| `_schema.circle` | Array di [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive una regione circolare con un raggio specifico centrato su una coordinata geografica. |
| `_schema.polygon` | [[!UICONTROL Cerchio geografico]](./geo-circle.md) | Serie di quattro o più coordinate in cui la prima e l&#39;ultima sono identiche. |
| `_schema.description` | Stringa | Descrizione di ciò che la forma definisce. |
| `_schema.elevation` | Doppio | L&#39;altezza specifica o minima della forma. Questo valore è conforme al [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e viene misurato in metri. In combinazione con `ceiling`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
| `_id` | Stringa | Identificatore univoco generato dal sistema per la forma. |
| `ceiling` | Doppio | La quota altimetrica massima della forma. Questa proprietà è valida solo se utilizzata in combinazione con `elevation`. Il valore è conforme al [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e viene misurato in metri. In combinazione con `elevation`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
