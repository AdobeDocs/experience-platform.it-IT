---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinates;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati Coordinate geografiche
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Coordinate geografiche.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 6%

---


# [!UICONTROL Geo Coordinates] tipo di dati

[!UICONTROL Geo Coordinates] è un tipo di dati XDM standard che descrive le coordinate geografiche di un luogo. Questo tipo di dati si basa sulle specifiche pubbliche documentate in [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.description` | Stringa | Descrizione dell&#39;identificazione delle coordinate. |
| `_schema.elevation` | Doppio | L&#39;elevazione specifica della coordinata definita. Il valore deve essere conforme al dato [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_schema.latitude` | Doppio | La coordinata verticale firmata del punto geografico. |
| `_schema.longitude` | Doppio | La coordinata orizzontale firmata del punto geografico. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
