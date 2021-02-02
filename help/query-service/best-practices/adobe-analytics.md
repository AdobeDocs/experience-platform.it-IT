---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;query di esempio;query di esempio;analisi adobe;'
solution: Experience Platform
title: Query di esempio
topic: queries
description: I dati provenienti da suite di rapporti Adobe Analytics selezionate  vengono trasformati in XDM ExperienceEvents e quindi trasferiti in Adobe Experience Platform come set di dati. In questo documento vengono illustrati alcuni casi di utilizzo in cui Adobe Experience Platform Query Service utilizza questi dati e le query di esempio incluse devono essere compatibili con i set di dati Adobe Analytics .
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# Query di esempio per  dati Adobe Analytics

I dati di  suite di rapporti Adobe Analytics selezionate vengono trasformati in dati conformi alla classe [!DNL XDM ExperienceEvent] e quindi trasferiti in Adobe Experience Platform come set di dati.

In questo documento vengono illustrati alcuni casi d&#39;uso in cui Adobe Experience Platform [!DNL Query Service] utilizza questi dati, incluse le query di esempio che devono funzionare con i set di dati Adobe Analytics . Per ulteriori informazioni sulla mappatura a [Analytics field mapping](../../sources/connectors/adobe-applications/mapping/analytics.md), consulta la documentazione relativa alla [!DNL Experience Events].

## Introduzione

Gli esempi SQL presenti in questo documento richiedono la modifica dell&#39;SQL e la compilazione dei parametri previsti per le query in base al dataset,  eVar, evento o intervallo di tempo che si desidera valutare. Fornire i parametri ovunque si trovi `{ }` negli esempi SQL che seguono.

## Esempi SQL usati comunemente

Gli esempi seguenti mostrano le query SQL comunemente utilizzate per analizzare i dati Adobe Analytics .

### Conteggio orario dei visitatori per un dato giorno

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### Le prime 10 pagine visualizzate per un dato giorno

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### Primi 10 utenti più attivi

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### Principali 10 città per attività utente

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### Primi 10 prodotti visualizzati

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

### Primi 10 ricavi totali ordine

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

### Conteggio eventi per giorno

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## Variabili di merchandising (sintassi del prodotto)


### Sintassi del prodotto

In  Adobe Analytics, i dati personalizzati a livello di prodotto possono essere raccolti tramite variabili configurate appositamente denominate variabili merchandising. Questi si basano su un eVar  o su eventi personalizzati. La differenza tra queste variabili e il loro uso standard è che rappresentano un valore separato per ogni prodotto trovato nell’hit, anziché un solo valore per l’hit.

Queste variabili sono denominate variabili merchandising della sintassi di prodotto. Questo consente la raccolta di informazioni, ad esempio un &quot;importo sconto&quot; per ogni prodotto o informazioni sulla &quot;posizione sulla pagina&quot; del prodotto nei risultati di ricerca del cliente.

Per ulteriori informazioni sull&#39;utilizzo della sintassi del prodotto, consultare la documentazione  Adobe Analytics in [implementazione di eVar utilizzando la sintassi del prodotto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Le sezioni seguenti descrivono i campi XDM necessari per accedere alle variabili di merchandising nel set di dati [!DNL Analytics]:

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Indice della matrice a cui si accede.
- `evar#`: Variabile  eVar specifica a cui si accede.

#### Eventi personalizzati

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Indice della matrice a cui si accede.
- `event#`: La specifica variabile evento personalizzata a cui si accede.

#### Query di esempio

Di seguito è riportata una query di esempio che restituisce un eVar e un evento  merchandising per il primo prodotto trovato in `productListItems`.

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

Questa query successiva esplode l&#39;array `productListItems` e restituisce ogni merchandising  eVar ed evento per prodotto. Il campo `_id` è incluso per mostrare la relazione con l’hit originale. Il valore `_id` è una chiave primaria univoca per il dataset.

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> Se si tenta di recuperare un campo che non esiste nel set di dati corrente, si verificherà l&#39;errore &quot;Nessun campo struttura&quot;. Valutare il motivo restituito nel messaggio di errore per identificare un campo disponibile, quindi aggiornare la query ed eseguire nuovamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintassi di conversione

Un altro tipo di variabile merchandising presente in  Adobe Analytics è la sintassi di conversione. Con la sintassi del prodotto, il valore viene raccolto contemporaneamente al prodotto, ma ciò richiede che i dati siano presenti sulla stessa pagina. Esistono scenari in cui i dati si verificano su una pagina prima della conversione o dell’evento di interesse relativo al prodotto. Ad esempio, prendere in considerazione il caso di utilizzo per il metodo di ricerca dei prodotti.

1. Un utente esegue una ricerca interna per &quot;cappello invernale&quot; che imposta il merchandising abilitato per la sintassi di conversione  eVar6 su &quot;ricerca interna:cappello invernale&quot;
2. L&#39;utente fa clic su &quot;waffle beanie&quot; e arriva sulla pagina dei dettagli del prodotto.\
   a. Qui di destinazione si attiva un evento `Product View` per il &quot;waffle beanie&quot; per $12.99.\
   b. Poiché `Product View` è configurato come un evento di binding, il prodotto &quot;waffle beanie&quot; è ora associato al valore di  eVar6 &quot;internal search:Winter hat&quot;. Ogni volta che il prodotto &quot;waffle beanie&quot; viene raccolto, viene associato a &quot;internal search:Winter hat&quot; fino a quando (1) viene raggiunta l&#39;impostazione di scadenza o (2) viene impostato un nuovo valore  eVar6 e l&#39;evento di binding si verifica nuovamente con quel prodotto.
3. L&#39;utente aggiunge il prodotto al carrello attivando l&#39;evento `Cart Add`.
4. L&#39;utente esegue un&#39;altra ricerca interna per &quot;summer shirt&quot; che imposta Conversione Syntax abilitato Merchandising  eVar6 su &quot;internal search:summer shirt&quot;
5. L&#39;utente clicca su &quot;sportiva t-shirt&quot; e atterra sulla pagina dei dettagli del prodotto.\
   a. A questo punto è attivato un evento `Product View` per &quot;sportiva t-shirt per $19.99.\
   b. L&#39;evento `Product View` è ancora il nostro evento di rilegatura, quindi ora il prodotto &quot;sportivo t-shirt&quot; è legato al valore di  eVar6 di &quot;ricerca interna:camicia estiva&quot; e il precedente prodotto &quot;waffle beanie&quot; è ancora legato a un  valore di eVar 6 di &quot;ricerca interna:waffle beanie&quot;.
6. L&#39;utente aggiunge il prodotto al carrello attivando l&#39;evento `Cart Add`.
7. L&#39;utente esegue il check-out con entrambi i prodotti.

Nel reporting, gli ordini, le entrate, le visualizzazioni dei prodotti e gli importi del carrello verranno riportati rispetto &#39;eVar 6 e verranno allineati all&#39;attività del prodotto associato.

|  eVar 6 (metodo di ricerca dei prodotti) | ricavo | order | viste prodotto | aggiunta carrello |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| ricerca interna:camicia estiva | 19,99 | 1 | 3 | 1 |
| ricerca interna:cappello invernale | 12,99 | 3 | 1 | 1 |

Per ulteriori informazioni sull&#39;utilizzo della sintassi di conversione, consultare la documentazione di Adobe Analytics  in [implementazione di eVar utilizzando la sintassi di conversione](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Di seguito sono riportati i campi XDM per generare la sintassi di conversione nel set di dati [!DNL Analytics]:

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: Variabile  eVar specifica a cui si accede.

#### Prodotto

```console
productListItems[#].sku
```

- `#`: Indice della matrice a cui si accede.

#### Query di esempio

Di seguito è riportata una query di esempio che esegue il binding del valore con la coppia prodotto/evento specifica, in questo caso l&#39;evento visualizzazione prodotto.

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

Di seguito è riportata una query di esempio che persiste il valore associato alle occorrenze successive del prodotto corrispondente. La sottoquery più bassa stabilisce la relazione tra i valori e il prodotto nell&#39;evento di binding dichiarato. La sottoquery successiva esegue l&#39;attribuzione di tale valore associato nelle successive interazioni con il rispettivo prodotto. E la selezione di livello principale aggrega i risultati per generare il reporting.

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```
