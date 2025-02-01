---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;circle;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati Cerchio geografico
description: Scopri il tipo di dati XDM Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 11%

---

# Tipo di dati [!UICONTROL Geo Circle]

[!UICONTROL Geo Circle] è un tipo di dati XDM standard che descrive l&#39;area geografica circolare, dato un particolare raggio centrato su un set specifico di coordinate. Questo tipo di dati è basato sulla specifica pubblica documentata in [schema.org](https://schema.org/GeoCircle).

![](../images/data-types/geo-circle.png){width=400}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive le coordinate geografiche del centro del cerchio. |
| `_schema.description` | Stringa | Una descrizione di cosa contiene il cerchio. |
| `_schema.radius` | Doppio | La lunghezza del raggio del cerchio. Questo valore è conforme al dato [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_id` | Stringa | ID univoco generato dal sistema per il cerchio. |
