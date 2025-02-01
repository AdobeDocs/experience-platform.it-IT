---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;poi;interazione;punto di interesse;punto di interesse;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati interazione punto di interesse
description: Scopri il tipo di dati XDM per l’interazione del punto di interesse.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL Tipo di dati interazione punto di interesse]

[!UICONTROL Interazione punto di interesse] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica informazioni di identità alle applicazioni mobili quando i dispositivi mobili rientrano nell&#39;intervallo.

![](../images/data-types/poi-interaction.png){width=400}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Dettagli punto di interesse]](./poi-details.md) | Descrive i dettagli del punto di interesse (POI) che ha causato l’evento. |
| `poiEntries` | Oggetto | Descrive il numero di volte in cui una persona è entrata nel POI. Contiene due proprietà: <ul><li>`id`: identificatore univoco della misura.</li><li>`value`: valore quantificabile della misura.</li></ul> |
| `poiExits` | Oggetto | Descrive il numero di volte in cui una persona è uscita dal POI. Contiene due proprietà: <ul><li>`id`: identificatore univoco della misura.</li><li>`value`: valore quantificabile della misura.</li></ul> |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
