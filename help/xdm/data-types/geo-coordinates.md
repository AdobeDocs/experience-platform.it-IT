---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;geo;coordinate;tipo di dati;tipo di dati;tipo di dati;home;popular topic;schema;Schema;XDM;fields;schemas;Schemas;geo;coordinate;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati Coordinate geografiche
description: Scopri il tipo di dati XDM Coordinate geografiche.
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 7%

---

# [!UICONTROL Coordinate geografiche] tipo di dati

[!UICONTROL Coordinate geografiche] è un tipo di dati XDM standard che descrive le coordinate geografiche di un luogo. Questo tipo di dati si basa sulla specifica pubblica documentata in [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_schema.description` | Stringa | Una descrizione di ciò che identificano le coordinate. |
| `_schema.elevation` | Doppio | L&#39;elevazione specifica della coordinata definita. Il valore deve essere conforme al [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) e viene misurato in metri. |
| `_schema.latitude` | Doppio | La coordinata verticale con segno del punto geografico. |
| `_schema.longitude` | Doppio | Coordinata orizzontale con segno del punto geografico. |
| `_id` | Stringa | ID univoco generato dal sistema per le coordinate. |
