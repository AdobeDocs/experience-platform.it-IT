---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati marketing
description: Questo documento fornisce una panoramica del tipo di dati Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---

# [!UICONTROL Marketing] tipo di dati

[!UICONTROL Marketing] è un tipo di dati XDM standard che descrive le attività di marketing attive con un particolare punto di contatto.

![](../images/data-types/marketing.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignGroup` | Stringa | Nome del gruppo di campagne (se più campagne sono raggruppate insieme come `50%_DISCOUNT`). |
| `campaignName` | Stringa | Nome della campagna di marketing, ad esempio `50%_DISCOUNT_USA` o `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Stringa | Il codice di tracciamento che può essere utilizzato per identificare la campagna di marketing a cui è associato l’evento. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
