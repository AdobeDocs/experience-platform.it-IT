---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: Inserisci tipo di dati contestuali
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Place Context.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 4%

---


# [!UICONTROL Place context] tipo di dati

[!UICONTROL Place context] è un tipo di dati XDM standard che descrive la posizione di un evento osservato, incluse le informazioni sul punto di interesse e le coordinate geografiche.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Descrive i dettagli relativi all’interazione punto di interesse (POI). |
| `activePOIs` | Matrice di [[!UICONTROL Point of interest details]](./poi-details.md) | Descrive i POI che hanno causato l’evento. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Descrive la posizione geografica in cui è stata distribuita l&#39;esperienza. |
| `localTime` | DateTime | Una marca temporale in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) , che indica l&#39;ora locale utilizzata con un offset del fuso orario dichiarato. Il pattern di formattazione è `yyyy-MM-dd'T'HH:mm:ssXXX` (ad esempio, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Intero | L&#39;offset del fuso orario locale corrente, espresso in minuti dall&#39;UTC, per il `localTime` valore. Deve includere l&#39;offset DST corrente, se applicabile. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)