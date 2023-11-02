---
title: Restituire e utilizzare le variabili di merchandising dai dati di analisi
description: Scopri come fornire campi XDM e query di esempio per accedere alle variabili di merchandising nei set di dati di Analytics.
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 3%

---

# Restituire e utilizzare le variabili di merchandising dai dati di Analytics

Utilizza Query Service per gestire i dati acquisiti da Adobe Analytics in Adobe Experience Platform come set di dati. Le sezioni seguenti forniscono query di esempio che puoi utilizzare per accedere alle variabili di merchandising nei set di dati di Analytics. Consulta la documentazione per ulteriori informazioni su [come acquisire e mappare i dati di Adobe Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) tramite l’origine Analytics

## Variabili merchandising {#merchandising-variables}

Le variabili di merchandising possono seguire una delle due sintassi seguenti:

* **Sintassi prodotto**: associa il valore eVar a un prodotto. 
* **Sintassi per variabile di conversione**: associa l’eVar a un prodotto solo se si verifica un evento di binding. È possibile selezionare gli eventi che fungono da eventi di binding.

## Sintassi del prodotto {#product-syntax}

In Adobe Analytics, i dati personalizzati a livello di prodotto possono essere raccolti tramite variabili appositamente configurate, denominate variabili di merchandising. Questi sono basati su un evento eVar o personalizzato. La differenza tra queste variabili e il loro utilizzo tipico è che rappresentano un valore separato per ogni prodotto trovato sull’hit, anziché un solo valore per l’hit.

Queste variabili sono denominate variabili di merchandising della sintassi di prodotto. Ciò consente la raccolta di informazioni, ad esempio un &quot;importo di sconto&quot; per prodotto o informazioni sulla &quot;posizione nella pagina&quot; del prodotto nei risultati di ricerca del cliente.

Per ulteriori informazioni sull’utilizzo della sintassi di prodotto, consulta la documentazione di Adobe Analytics su [implementazione di eVar utilizzando la sintassi di prodotto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

Le sezioni seguenti descrivono i campi XDM necessari per accedere alle variabili di merchandising nel [!DNL Analytics] set di dati:

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: indice dell’array a cui si sta effettuando l’accesso.
* `evar#`: variabile eVar specifica a cui stai effettuando l’accesso.

### Eventi personalizzati

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: indice dell’array a cui si sta effettuando l’accesso.
* `event#`: variabile evento personalizzata specifica a cui stai effettuando l’accesso.

## Casi di utilizzo della sintassi di prodotto {#product-use-cases}

I seguenti casi d’uso si concentrano sulla restituzione di un eVar di merchandising dal `productListItems` array utilizzando SQL.

### Restituire un eVar e un evento di merchandising

La query seguente restituisce un eVar e un evento di merchandising per il primo prodotto trovato in `productListItems` array.

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

### Esplodi l’array productListItems e restituisce l’eVar e l’evento di merchandising per ciascun prodotto.

Questa query successiva esplode `productListItems` e restituisce ogni eVar e evento di merchandising per prodotto. Il `_id` Questo campo è incluso per mostrare la relazione con l’hit originale. Il `_id` value è una chiave primaria univoca per il set di dati.

>[!NOTE]
>
>La funzione di esplosione separa gli elementi di un array in più righe. Sono esclusi i valori nulli.

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
> Se tenti di recuperare un campo che non esiste nel set di dati corrente, si verifica l’errore &quot;Nessun campo struct simile&quot;. Valuta il motivo restituito nel messaggio di errore per identificare un campo disponibile, quindi aggiorna la query ed eseguila di nuovo.
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintassi per variabile di conversione {#conversion-variable-syntax}

Un altro tipo di variabile di merchandising che si trova in Adobe Analytics è la sintassi per variabile di conversione. La sintassi per le variabili di conversione viene utilizzata quando il valore eVar non è disponibile per essere impostato nella variabile prodotti. Generalmente, questo scenario indica che la pagina non contiene nessun contesto del canale di merchandising o del metodo di ricerca. In questi casi, è necessario impostare la variabile merchandising prima che l’utente arrivi alla pagina del prodotto e il valore persiste finché non si verifica l’evento di binding.

Ad esempio, lo scenario di ricerca dei prodotti riportato di seguito illustra come i dati richiesti possono essere presenti in una pagina prima che si verifichi la conversione o l’evento correlato al prodotto.

1. Un utente esegue una ricerca interna di &quot;cappello invernale&quot; che imposta la sintassi di conversione abilitata per merchandising eVar6 su &quot;internal search:winter hat&quot; (ricerca interna:cappello invernale).
2. L’utente fa clic su &quot;waffle beanie&quot; e arriva alla pagina dei dettagli del prodotto.\
   a. L’atterraggio qui viene attivato da un `Product View` evento per il &quot;waffle beanie&quot; per $ 12,99.\
   b. Dal `Product View` è configurato come evento di binding, il prodotto &quot;waffle beanie&quot; è ora associato al valore eVar6 &quot;internal search:winter hat&quot;. Ogni volta che il prodotto &quot;waffle beanie&quot; viene raccolto, è associato a &quot;ricerca interna:cappello invernale&quot;. Questo accade finché non viene raggiunta l’impostazione di scadenza eVar oppure finché non viene impostato un nuovo valore eVar6 e l’evento di binding si verifica di nuovo con quel prodotto.
3. L’utente aggiunge il prodotto al carrello, attivando `Cart Add` evento.
4. L’utente esegue un’altra ricerca interna di &quot;camicia estiva&quot; che imposta la sintassi di conversione abilitata per merchandising eVar6 su &quot;internal search:summer shirt&quot; (ricerca interna:camicia estiva).
5. L’utente seleziona la &quot;t-shirt sportiva&quot; e arriva alla pagina dei dettagli del prodotto.\
   a. L’atterraggio qui viene attivato da un `Product View` evento per &quot;sporty t-shirt per $19.99.\
   b. In quanto `Product View` evento è l&#39;evento di binding, il prodotto &quot;sporty t-shirt&quot; è ora associato al valore eVar6 di &quot;internal search:summer shirt&quot;. Il prodotto precedente &quot;waffle beanie&quot; è ancora associato a un valore eVar6 &quot;internal search:waffle beanie&quot;.
6. L’utente aggiunge il prodotto al carrello, attivando `Cart Add` evento.
7. L’utente estrae con entrambi i prodotti.

Nella generazione rapporti, gli ordini, i ricavi, le visualizzazioni dei prodotti e le aggiunte al carrello sono soggetti a reporting a fronte di eVar6 e sono allineati all’attività del prodotto associato.

| eVar6 (metodo di ricerca del prodotto) | ricavi | ordini | visualizzazioni prodotto | aggiunte al carrello |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| ricerca interna:camicia estiva | 19,99 | 1 | 1 | 1 |
| ricerca interna:cappello invernale | 12.99 | 1 | 1 | 1 |

Per ulteriori informazioni sull’utilizzo della sintassi per le variabili di conversione, consulta la documentazione di Adobe Analytics su [implementazione delle eVar tramite la sintassi per le variabili di conversione](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Di seguito sono riportati i campi XDM per produrre la sintassi della variabile di conversione nel [!DNL Analytics] set di dati:

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: variabile eVar specifica a cui stai effettuando l’accesso.

#### Prodotto

```console
productListItems[#].sku
```

* `#`: indice dell’array a cui si sta effettuando l’accesso.

## Casi di utilizzo della variabile di conversione {#conversion-variable-use-cases}

I casi d’uso riportati di seguito riflettono scenari che richiedono una sintassi per le variabili di conversione.

### Associa il valore alla coppia di prodotti ed eventi specifica

La query seguente associa il valore alla coppia di prodotti ed eventi specifica. In questo esempio, il valore è associato all’evento di visualizzazione prodotto.

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

### Mantenere il valore associato alle occorrenze successive del rispettivo prodotto

La query di esempio seguente mantiene il valore associato alle occorrenze successive del rispettivo prodotto. La sottoquery più bassa stabilisce la relazione del valore con il prodotto nell’evento di binding dichiarato. La sottoquery successiva esegue l’attribuzione di tale valore associato nelle interazioni successive con il rispettivo prodotto. Il livello superiore SELECT aggrega i risultati per produrre il reporting.

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

## Passaggi successivi

Una volta letto questo documento, sarai in grado di capire meglio come restituire un eVar di merchandising utilizzando la sintassi del prodotto e associare un valore a un prodotto specifico con la sintassi della variabile di conversione.

Se non lo hai già fatto, leggi la sezione [Documentazione di Analytics Insights for web and mobile interactions](./analytics-insights.md) avanti. Vengono forniti casi d’uso comuni e viene illustrato come utilizzare Query Service per creare informazioni fruibili dai dati di Adobe Analytics per web e dispositivi mobili.
