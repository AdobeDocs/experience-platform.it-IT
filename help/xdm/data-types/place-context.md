---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;posizionare contesto;placeContext;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Inserisci tipo di dati contestuali
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati Inserisci contesto XDM.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 4%

---

# [!UICONTROL Place context] tipo di dati

[!UICONTROL Place context] è un tipo di dati XDM standard che descrive la posizione di un evento osservato, comprese le informazioni sui punti di interesse e le coordinate geografiche.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Point of interest interaction]](./poi-interaction.md) | Descrive i dettagli dell’interazione punto-di-interesse (POI). |
| `activePOIs` | Array di [[!UICONTROL Point of interest details]](./poi-details.md) | Descrive i punti di interesse che hanno causato l’evento. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Descrive la posizione geografica in cui è stata distribuita l&#39;esperienza. |
| `localTime` | DateTime | Una marca temporale in formato [RFC 3339](https://tools.ietf.org/html/rfc3339) che indica l&#39;ora locale che utilizza con un offset del fuso orario specificato. Il pattern di formattazione è `yyyy-MM-dd'T'HH:mm:ssXXX` (ad esempio, `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Intero | Offset del fuso orario locale corrente in minuti da UTC per il valore `localTime`. Questo dovrebbe includere l&#39;offset DST corrente, se applicabile. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
