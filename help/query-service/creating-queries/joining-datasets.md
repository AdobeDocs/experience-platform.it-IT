---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unione di set di dati
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '53'
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
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![Immagine](../images/queries/joining-datasets/select-operating-systems.png)