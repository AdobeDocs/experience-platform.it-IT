---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;inserire contesto;placeContext;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati contestuali del luogo
description: Scopri il tipo di dati XDM Place Context.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 3%

---

# [!UICONTROL Inserisci tipo di dati contesto]

[!UICONTROL Contesto luogo] è un tipo di dati XDM standard che descrive la posizione di un evento osservato, incluse le informazioni sui punti di interesse e le coordinate geografiche.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interazione punto di interesse]](./poi-interaction.md) | Descrive i dettagli dell’interazione del punto di interesse (POI). |
| `activePOIs` | Array di [[!UICONTROL Dettagli punto di interesse]](./poi-details.md) | Descrive i POI che hanno causato l&#39;evento. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Descrive la posizione geografica in cui è stata distribuita l’esperienza. |
| `localTime` | Data e ora | Un timestamp in formato [RFC 3339](https://tools.ietf.org/html/rfc3339), che indica l&#39;ora locale utilizzando con uno scostamento fuso orario dichiarato. Il pattern di formattazione è `yyyy-MM-dd'T'HH:mm:ssXXX` (ad esempio, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Intero | Offset del fuso orario locale corrente in minuti da UTC per il valore `localTime`. Questo dovrebbe includere l&#39;offset DST corrente, se applicabile. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
