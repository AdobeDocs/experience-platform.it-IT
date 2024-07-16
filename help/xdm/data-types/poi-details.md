---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;poi;dettagli poi;punto di interesse;dettagli punto di interesse;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati Dettagli punto di interesse
description: Scopri il tipo di dati XDM dei dettagli dei punti di interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 15%

---

# [!UICONTROL Dettagli punto di interesse] tipo di dati

[!UICONTROL Dettagli punto di interesse] è un tipo di dati XDM standard che descrive i dati relativi alla posizione geografica in cui è stato osservato un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descrive i dettagli del beacon attivi per l’interazione con il punto di interesse (POI). |
| `geoInteractionDetails` | [[!UICONTROL Dettagli interazione geografica]](./geo-interaction-details.md) | Descrive i dettagli geografici attivi per l’interazione con i punti di interesse (POI). |
| `category` | Stringa | Categoria generale assegnata per organizzare i POI dall’amministratore delle definizioni dei POI. |
| `distanceToPOICenter` | Doppio | La distanza stimata dal centro del punto di interesse (POI) in metri. |
| `locatingType` | Stringa | Meccanismo utilizzato per determinare la posizione. I valori accettati includono: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Stringa | Nome assegnato al punto di interesse (POI). |
| `poiID` | Stringa | Un identificatore univoco del POI. |
| `type` | Stringa | Il tipo generale del punto di interesse (POI) che utilizza uno schema di digitazione selezionato dall’amministratore delle definizioni dei POI. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
