---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;beacon;dettagli interazione;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati Dettagli interazione geografica
description: Scopri il tipo di dati XDM dei dettagli di interazione geografica.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL Dettagli dell’interazione geografica] tipo di dati

[!UICONTROL Dettagli dell’interazione geografica] è un tipo di dati XDM standard che descrive lo stato corrente di inclusione in un’area geografica definita.

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forma di geotargeting]](./geo-shape.md) | Descrive la forma geografica dell’area con cui si interagisce. Questo campo può descrivere una casella, un cerchio o un poligono. |
| `deviceGeoAccuracy` | Doppio | La precisione del dispositivo o meccanismo di misurazione geografica, misurata in metri. |
| `distanceToCenter` | Doppio | La distanza dal centro dell&#39;area geografica nel caso di un cerchio geografico, misurata in metri. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
