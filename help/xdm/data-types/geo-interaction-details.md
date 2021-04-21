---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;beacon;dettagli interazione;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati dettagli interazione geografica
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Dettagli interazione geografica.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 2%

---

# [!UICONTROL Geo interaction details] tipo di dati

[!UICONTROL Geo interaction details] è un tipo di dati XDM standard che descrive lo stato corrente di inclusione in un’area geograficamente definita.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Geo Shape]](./geo-shape.md) | Descrive la forma geografica dell&#39;area con cui viene interagito. Questo campo può descrivere una scatola, un cerchio o un poligono. |
| `deviceGeoAccuracy` | Doppio | La precisione del dispositivo o meccanismo di misurazione del geo, misurata in metri. |
| `distanceToCenter` | Doppio | La distanza dal centro di geo nel caso di un cerchio geografico, misurata in metri. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
