---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati dettagli interazione geografica
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Dettagli interazione geografica.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---


# [!UICONTROL Geo interaction details] tipo di dati

[!UICONTROL Geo interaction details] è un tipo di dati XDM standard che descrive lo stato corrente di inclusione in un&#39;area geograficamente definita.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | Descrive la forma geografica dell&#39;area con cui viene interagito. Questo campo può descrivere una casella, un cerchio o un poligono. |
| `deviceGeoAccuracy` | Doppio | La precisione del dispositivo o meccanismo di misurazione del geo, misurata in metri. |
| `distanceToCenter` | Doppio | La distanza dal centro del geo nel caso di un cerchio geografico, misurata in metri. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
