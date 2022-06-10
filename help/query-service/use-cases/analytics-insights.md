---
title: 'Informazioni approfondite su Analytics per le interazioni web e mobile '
description: Questo documento spiega come utilizzare Query Service per creare informazioni fruibili dai dati Adobe Analytics acquisiti.
source-git-commit: cdceba9caf035831f4c376edf34356f666b79aa8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---

# Informazioni di Analytics per le interazioni web e mobile

Adobe Experience Platform consente di acquisire dati dalle suite di rapporti Adobe Analytics utilizzando i campi Experience Data Model (XDM) per compilare i set di dati. Query Service può quindi utilizzare questi dati di analisi eseguendo query SQL per generare informazioni utili da un comportamento degli utenti sulle piattaforme digitali.

Questo documento fornisce una serie di query SQL di esempio che mostrano casi d&#39;uso comuni durante la creazione di informazioni dai dati di analisi web e mobili.

Consulta la sezione [Documentazione sulle mappature dei campi di Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) per ulteriori informazioni sull’acquisizione e la mappatura dei dati analitici.

## Introduzione

Per ciascuno dei seguenti casi d&#39;uso, viene fornito un esempio di query SQL con parametri come modello da personalizzare. Fornisci parametri ovunque vedi `{ }` negli esempi SQL per il set di dati, l&#39;eVar, l&#39;evento o l&#39;intervallo di tempo che si desidera valutare.

## Obiettivi

Gli esempi seguenti mostrano le query SQL per i casi d&#39;uso comuni per analizzare i dati di Adobe Analytics.

### Genera il conteggio dei visitatori per ogni ora in un dato giorno

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour,
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Identifica le 10 pagine più visualizzate in un dato giorno

```SQL
SELECT web.webpagedetails.name AS Page_Name,
       Sum(web.webpagedetails.pageviews.value) AS Page_Views
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name
ORDER BY page_views DESC
LIMIT  10;
```

### Identificare i 10 utenti più attivi

```sql
SELECT enduserids._experience.aaid.id AS aaid,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Identifica le 10 città più desiderate in base all’attività dell’utente

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city,
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Identificare i 10 prodotti più visualizzati

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU,
              commerce.productviews.value   AS Product_Views
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
              AND commerce.productviews.value IS NOT NULL)
GROUP BY Product_SKU
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### Identificare i 10 ricavi più elevati

```sql
SELECT Purchase_ID,
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID,
               Explode(productlistitems)   AS Product_Items
        FROM   {TARGET_TABLE}
        WHERE  commerce.`order`.purchaseid IS NOT NULL
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID
ORDER BY total_order_revenue DESC
LIMIT  10;
```
