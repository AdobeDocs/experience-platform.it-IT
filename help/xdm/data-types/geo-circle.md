---
keywords: Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;schemi;schemi;geo;cerchio;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati del cerchio geografico
description: Questo documento fornisce una panoramica del tipo di dati XDM di Geo Circle.
exl-id: fa041f4f-9955-44e9-b235-a643e07d402c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 5%

---

# [!UICONTROL Cerchio geografico] tipo di dati

[!UICONTROL Cerchio geografico] è un tipo di dati XDM standard che descrive una regione geografica circolare, in base a un raggio particolare centrato su un insieme specifico di coordinate. Questo tipo di dati si basa sulle specifiche pubbliche documentate in [schema.org](https://schema.org/GeoCircle).

<img src="../images/data-types/geo-circle.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.coordinates` | [[!UICONTROL Coordinate geografiche]](./geo-coordinates.md) | Descrive le coordinate geografiche del centro del cerchio. |
| `_schema.description` | Stringa | Descrizione del contenuto del cerchio. |
| `_schema.radius` | Doppio | Lunghezza del raggio del cerchio. Questo valore è conforme al [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e viene misurato in metri. |
| `_id` | Stringa | Un ID univoco generato dal sistema per il cerchio. |
