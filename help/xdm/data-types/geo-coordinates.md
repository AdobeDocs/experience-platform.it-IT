---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;schemi;geo;coordinate;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati coordinate geografiche
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Coordinate geografiche.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---


# [!UICONTROL Geo Coordinates] tipo di dati

[!UICONTROL Geo Coordinates] è un tipo di dati XDM standard che descrive le coordinate geografiche di un luogo. Questo tipo di dati è basato sulle specifiche pubbliche documentate in [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.description` | Stringa | Descrizione dell&#39;identificazione delle coordinate. |
| `_schema.elevation` | Doppio | L&#39;elevazione specifica della coordinata definita. Il valore deve essere conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_schema.latitude` | Doppio | La coordinata verticale firmata del punto geografico. |
| `_schema.longitude` | Doppio | La coordinata orizzontale firmata del punto geografico. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
