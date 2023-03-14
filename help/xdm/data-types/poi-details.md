---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;poi;dettagli poi;punto di interesse;dettagli punto di interesse;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati Dettagli punto di interesse
description: Questo documento fornisce una panoramica del tipo di dati XDM per i dettagli dei punti di interesse.
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# [!UICONTROL Dettagli del punto di interesse] tipo di dati

[!UICONTROL Dettagli del punto di interesse] è un tipo di dati XDM standard che descrive i dati geografici in cui è stato osservato un evento.

<img src="../images/data-types/poi-details.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | Descrive i dettagli del beacon attivi per l’interazione con il punto di interesse (POI). |
| `geoInteractionDetails` | [[!UICONTROL Dettagli dell’interazione geografica]](./geo-interaction-details.md) | Descrive i dettagli geografici attivi per l’interazione con i punti di interesse (POI). |
| `category` | Stringa | Categoria generale assegnata per organizzare i POI dall’amministratore delle definizioni dei POI. |
| `distanceToPOICenter` | Doppio | La distanza stimata dal centro del punto di interesse (POI) in metri. |
| `locatingType` | Stringa | Meccanismo utilizzato per determinare la posizione. I valori accettati includono: <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | Stringa | Nome assegnato al punto di interesse (POI). |
| `poiID` | Stringa | Un identificatore univoco del POI. |
| `type` | Stringa | Il tipo generale del POI che utilizza uno schema di digitazione selezionato dall’amministratore delle definizioni dei POI. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
