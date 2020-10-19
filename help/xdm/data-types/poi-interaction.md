---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;poi;interaction;point of interest;point-of-interest;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati di interazione punto di interesse
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM interazione punto di interesse.
translation-type: tm+mt
source-git-commit: 032adc72db7f094b268f14e8f7d48810830a84e4
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---


# [!UICONTROL Point of interest interaction] tipo di dati

[!UICONTROL Point of interest interaction] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica le informazioni di identità alle applicazioni mobili man mano che i dispositivi mobili rientrano nell&#39;intervallo.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Descrive i dettagli del POI che ha causato l’evento. |
| `poiEntries` | Oggetto | Descrive il numero di volte in cui una persona è entrata nel POI. Contiene due proprietà: <ul><li>`id`: Un identificatore univoco per la misura.</li><li>`value`: Il valore quantificabile della misura.</li></ul> |
| `poiExits` | Oggetto | Descrive il numero di volte in cui una persona è uscita dal POI. Contiene due proprietà: <ul><li>`id`: Un identificatore univoco per la misura.</li><li>`value`: Il valore quantificabile della misura.</li></ul> |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
