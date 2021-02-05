---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;schemi;geo;cerchio;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo di dati del cerchio geografico
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Geo Circle.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---


# [!UICONTROL Geo Circle] tipo di dati

[!UICONTROL Geo Circle] è un tipo di dati XDM standard che descrive l&#39;area geografica circolare, in base a un raggio particolare centrato su un insieme specifico di coordinate. Questo tipo di dati è basato sulle specifiche pubbliche documentate in [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive le coordinate geografiche del centro del cerchio. |
| `_schema.description` | Stringa | Descrizione del contenuto del cerchio. |
| `_schema.radius` | Doppio | Lunghezza del raggio del cerchio. Questo valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_id` | Stringa | Un ID univoco generato dal sistema per il cerchio. |
