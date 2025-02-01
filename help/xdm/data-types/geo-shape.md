---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;geo shape;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati forma geografica
description: Scopri il tipo di dati XDM Geo Shape.
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# [!UICONTROL Forma geografica] tipo di dati

[!UICONTROL Forma geografica] è un tipo di dati XDM standard che descrive la forma di un&#39;area geografica. Questo tipo di dati è basato sulla specifica pubblica documentata in [schema.org](https://schema.org/GeoShape).

![](../images/data-types/geo-shape.png){width=500}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.box` | Array di [[!UICONTROL coordinate geografiche]](./geo-coordinates.md) | Descrive un&#39;area geografica racchiusa da un rettangolo formato da due coordinate. La prima coordinata è l&#39;angolo inferiore del rettangolo e la seconda coordinata è l&#39;angolo superiore. |
| `_schema.circle` | Array di [[!UICONTROL coordinate geografiche]](./geo-coordinates.md) | Descrive una regione circolare con un raggio specifico centrato su una coordinata geografica. |
| `_schema.polygon` | [[!UICONTROL Cerchio geografico]](./geo-circle.md) | Serie di quattro o più coordinate in cui la prima e l&#39;ultima sono identiche. |
| `_schema.description` | Stringa | Una descrizione di ciò che la forma definisce. |
| `_schema.elevation` | Doppio | L&#39;altezza specifica o minima della forma. Questo valore è conforme al dato [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `ceiling`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
| `_id` | Stringa | Identificatore univoco generato dal sistema per la forma. |
| `ceiling` | Doppio | La quota altimetrica massima della forma. Questa proprietà è valida solo se utilizzata in combinazione con `elevation`. Il valore è conforme al dato [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. In combinazione con `elevation`, questa proprietà può essere utilizzata per esprimere un rettangolo di selezione tridimensionale per una posizione. |
