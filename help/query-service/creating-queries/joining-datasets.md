---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: Unione di set di dati
topic: queries
type: Tutorial
description: L'unione di set di dati consente di includere nella query i dati provenienti da altri set di dati. In questo esempio viene utilizzato un dataset del sistema operativo personalizzato per mappare l'ID del sistema operativo sul valore del sistema operativo.
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 1%

---


# Unione di set di dati

L&#39;unione di set di dati consente di includere nella query i dati provenienti da altri set di dati. In questo esempio viene utilizzato un dataset del sistema operativo personalizzato per mappare il `operatingsystemID` valore al `operatingsystem` valore.

Set di dati:
- your_analytics_table
- custom_operation_system_search

Create un&#39; `SELECT` istruzione per i primi 50 sistemi operativi in base al numero di visualizzazioni di pagina.

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Immagine](../images/queries/joining-datasets/select-operating-systems.png)