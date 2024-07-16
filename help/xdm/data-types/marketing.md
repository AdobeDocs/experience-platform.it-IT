---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di marketing
description: Scopri il tipo di dati Marketing XDM.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# Tipo di dati [!UICONTROL Marketing]

[!UICONTROL Marketing] è un tipo di dati XDM standard che descrive le attività di marketing attive con un particolare punto di contatto.

![](../images/data-types/marketing.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `campaignGroup` | Stringa | Il nome del gruppo della campagna (nei casi in cui più campagne siano raggruppate come `50%_DISCOUNT`). |
| `campaignName` | Stringa | Nome della campagna di marketing, ad esempio `50%_DISCOUNT_USA` o `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Stringa | Codice di tracciamento che può essere utilizzato per identificare la campagna di marketing a cui è associato l’evento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
