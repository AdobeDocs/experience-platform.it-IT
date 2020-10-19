---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;circle;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati Geo Circle
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Geo Circle.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 4%

---


# [!UICONTROL Geo Circle] tipo di dati

[!UICONTROL Geo Circle] è un tipo di dati XDM standard che descrive l&#39;area geografica circolare, in base a un raggio particolare centrato su un insieme specifico di coordinate. Questo tipo di dati si basa sulle specifiche pubbliche documentate in [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive le coordinate geografiche del centro del cerchio. |
| `_schema.description` | Stringa | Descrizione del contenuto del cerchio. |
| `_schema.radius` | Doppio | Lunghezza del raggio del cerchio. Questo valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_id` | Stringa | Un ID univoco generato dal sistema per il cerchio. |
