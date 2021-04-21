---
keywords: Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;schemi;schemi;geo;cerchio;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati del cerchio geografico
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM di Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 3%

---

# [!UICONTROL Geo Circle] tipo di dati

[!UICONTROL Geo Circle] è un tipo di dati XDM standard che descrive una regione geografica circolare, in base a un raggio particolare centrato su un insieme specifico di coordinate. Questo tipo di dati si basa sulle specifiche pubbliche documentate su [schema.org](http://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Descrive le coordinate geografiche del centro del cerchio. |
| `_schema.description` | Stringa | Descrizione del contenuto del cerchio. |
| `_schema.radius` | Doppio | Lunghezza del raggio del cerchio. Questo valore è conforme al Riferimento [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) ed è misurato in metri. |
| `_id` | Stringa | Un ID univoco generato dal sistema per il cerchio. |
