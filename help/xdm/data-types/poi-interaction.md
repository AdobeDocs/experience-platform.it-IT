---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;poi;interazione;punto di interesse;punto di interesse;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di interazione del punto di interesse
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM del punto di interesse per l’interazione.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!UICONTROL Point of interest interaction] tipo di dati

[!UICONTROL Point of interest interaction] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica le informazioni di identità alle applicazioni mobili man mano che i dispositivi mobili rientrano nella gamma.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Descrive i dettagli del POI che ha causato l’evento. |
| `poiEntries` | Oggetto | Descrive il numero di volte in cui una persona è entrata nel POI. Contiene due proprietà: <ul><li>`id`: Identificatore univoco della misura.</li><li>`value`: Valore quantificabile della misura.</li></ul> |
| `poiExits` | Oggetto | Descrive il numero di volte in cui una persona è uscita dal POI. Contiene due proprietà: <ul><li>`id`: Identificatore univoco della misura.</li><li>`value`: Valore quantificabile della misura.</li></ul> |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
