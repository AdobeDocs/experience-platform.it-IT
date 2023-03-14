---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;inserire contesto;placeContext;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati contestuali del luogo
description: Questo documento fornisce una panoramica del tipo di dati XDM Place Context.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 5%

---

# [!UICONTROL Contesto del luogo] tipo di dati

[!UICONTROL Contesto del luogo] è un tipo di dati XDM standard che descrive la posizione di un evento osservato, incluse informazioni sui punti di interesse e coordinate geografiche.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interazione del punto di interesse]](./poi-interaction.md) | Descrive i dettagli dell’interazione del punto di interesse (POI). |
| `activePOIs` | Array di [[!UICONTROL Dettagli del punto di interesse]](./poi-details.md) | Descrive i POI che hanno causato l&#39;evento. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Descrive la posizione geografica in cui è stata distribuita l’esperienza. |
| `localTime` | DateTime | Una marca temporale in [RFC 3339](https://tools.ietf.org/html/rfc3339) formato, che indica l’ora locale utilizzando con uno scostamento fuso orario dichiarato. Il pattern di formattazione è `yyyy-MM-dd'T'HH:mm:ssXXX` (ad esempio, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Intero | Lo scostamento del fuso orario locale corrente in minuti da UTC per `localTime` valore. Questo dovrebbe includere l&#39;offset DST corrente, se applicabile. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
