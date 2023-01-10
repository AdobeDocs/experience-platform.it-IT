---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;schemi;poi;dettagli;punto di interesse;dettagli del punto di interesse;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati dei dettagli del punto di interesse
description: Questo documento fornisce una panoramica del tipo di dati XDM dei dettagli del punto di interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 6%

---

# [!UICONTROL Dettagli del punto di interesse] tipo di dati

[!UICONTROL Dettagli del punto di interesse] è un tipo di dati XDM standard che descrive i dati relativi alla posizione geografica in cui è stato osservato un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descrive i dettagli del beacon attivi per l’interazione POI. |
| `geoInteractionDetails` | [[!UICONTROL Dettagli interazione geografica]](./geo-interaction-details.md) | Descrive i dettagli geografici attivi per l’interazione POI. |
| `category` | Stringa | Una categoria generale assegnata dall’amministratore delle definizioni dei punti di interesse per l’organizzazione dei punti di interesse. |
| `distanceToPOICenter` | Doppio | La distanza stimata dal centro POI in metri. |
| `locatingType` | Stringa | Meccanismo utilizzato per determinare la posizione. I valori accettati includono: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Stringa | Nome assegnato al POI. |
| `poiID` | Stringa | Identificatore univoco del POI. |
| `type` | Stringa | Il tipo generale del POI utilizzando uno schema di digitazione selezionato dall&#39;amministratore delle definizioni dei POI. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
