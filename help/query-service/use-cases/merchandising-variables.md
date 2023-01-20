---
title: Restituire e utilizzare le variabili merchandising dai dati di analisi
description: Scopri come fornire campi XDM e query di esempio per accedere alle variabili merchandising nei set di dati di Analytics.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# Restituire e utilizzare le variabili merchandising dai dati di analytics

Utilizza Query Service per gestire i dati acquisiti da Adobe Analytics in Adobe Experience Platform come set di dati. Le sezioni seguenti forniscono query di esempio che puoi utilizzare per accedere alle variabili di merchandising nei set di dati di Analytics. Per ulteriori informazioni, consulta la documentazione . [come acquisire e mappare i dati di Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=it) tramite la sorgente di Analytics

## Variabili merchandising {#merchandising-variables}

Le variabili di merchandising possono seguire una delle due sintassi seguenti:

* **Sintassi prodotto**: Associa il valore eVar a un prodotto. 
* **Sintassi della variabile di conversione**: Associa l’eVar a un prodotto solo se si verifica un evento di binding. È possibile selezionare gli eventi che fungono da eventi di binding.

## Sintassi del prodotto {#product-syntax}

In Adobe Analytics, i dati personalizzati a livello di prodotto possono essere raccolti attraverso variabili appositamente configurate denominate variabili merchandising. Sono basati su eventi eVar o personalizzati. La differenza tra queste variabili e il loro uso tipico è che rappresentano un valore separato per ogni prodotto trovato sull&#39;hit, anziché un solo valore per l&#39;hit.

Queste variabili sono denominate variabili di merchandising con sintassi di prodotto. Ciò consente la raccolta di informazioni, ad esempio un &quot;importo dello sconto&quot; per prodotto o informazioni sulla &quot;posizione sulla pagina&quot; del prodotto nei risultati di ricerca del cliente.

Per ulteriori informazioni sull’utilizzo della sintassi del prodotto, consulta la documentazione di Adobe Analytics in [implementazione di eVar utilizzando la sintassi del prodotto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

Le sezioni seguenti descrivono i campi XDM necessari per accedere alle variabili di merchandising nel tuo [!DNL Analytics] set di dati:

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`: Indice della matrice a cui si accede.
* `evar#`: Variabile eVar specifica a cui si accede.

### Eventi personalizzati

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`: Indice della matrice a cui si accede.
* `event#`: La variabile evento personalizzata specifica a cui si accede.

## Casi d’uso della sintassi del prodotto {#product-use-cases}

I seguenti casi d’uso si concentrano sulla restituzione di un eVar di merchandising dal `productListItems` array che utilizza SQL.

### Restituire un eVar e un evento di merchandising

La query seguente restituisce un eVar di merchandising e un evento per il primo prodotto trovato nella `productListItems` array.

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

### Esplodi la matrice productListItems e restituisce l&#39;eVar e l&#39;evento merchandising per ogni prodotto.

Questa successiva query esplode la `productListItems` e restituisce ogni eVar e evento di merchandising per prodotto. La `_id` Il campo è incluso per mostrare la relazione con l’hit originale. La `_id` value è una chiave primaria univoca per il set di dati.

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
> Se tenti di recuperare un campo che non esiste nel set di dati corrente, si verifica l’errore &quot;Nessun campo di struttura&quot;. Valutare il motivo restituito nel messaggio di errore per identificare un campo disponibile, quindi aggiornare la query ed eseguirla nuovamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintassi della variabile di conversione {#conversion-variable-syntax}

Un altro tipo di variabile di merchandising trovato in Adobe Analytics è la sintassi della variabile di conversione. La sintassi della variabile di conversione viene utilizzata quando il valore eVar non è disponibile per essere impostato nella variabile products . Generalmente, questo scenario indica che la pagina non contiene nessun contesto del canale di merchandising o del metodo di ricerca. In questi casi, è necessario impostare la variabile merchandising prima che l’utente arrivi alla pagina del prodotto, e il valore persiste finché non si verifica l’evento di binding.

Ad esempio, lo scenario di ricerca dei prodotti seguente illustra come i dati richiesti possono essere presenti in una pagina prima che si verifichi la conversione o l’evento relativo al prodotto.

1. Un utente esegue una ricerca interna per &quot;cappello invernale&quot; che imposta la sintassi di conversione abilitata merchandising eVar6 su &quot;ricerca interna:cappello invernale&quot;.
2. L&#39;utente clicca su &quot;waffle beanie&quot; e arriva sulla pagina dei dettagli del prodotto.\
   a) L&#39;atterraggio qui si attiva via un `Product View` evento per il &quot;waffle beanie&quot; per $12.99.\
   b) Da `Product View` è configurato come evento di binding, il prodotto &quot;waffle beanie&quot; è ora associato al valore eVar6 di &quot;internal search:Winter hat&quot;. Ogni volta che il prodotto &quot;waffle beanie&quot; viene raccolto, è associato a &quot;ricerca interna: cappello invernale&quot;. Ciò si verifica fino al raggiungimento dell’impostazione di scadenza eVar oppure quando viene impostato un nuovo valore eVar6 e l’evento di binding si verifica nuovamente con quel prodotto.
3. L’utente aggiunge il prodotto al carrello attivando la `Cart Add` evento.
4. L&#39;utente esegue un&#39;altra ricerca interna per &quot;Summer shirt&quot; che imposta la sintassi di conversione abilitata merchandising eVar6 su &quot;internal search:Summer shirt&quot;.
5. L&#39;utente seleziona &quot;sportivo t-shirt&quot; e atterra sulla pagina dei dettagli del prodotto.\
   a) L&#39;atterraggio qui si attiva via un `Product View` evento per &quot;t-shirt sportiva per $19.99.\
   b) Come `Product View` evento è l&#39;evento di associazione, il prodotto &quot;t-shirt sportiva&quot; è ora legato al valore eVar6 di &quot;ricerca interna:camicia estiva&quot;. Il prodotto precedente &quot;waffle beanie&quot; è ancora legato a un valore eVar6 di &quot;ricerca interna:waffle beanie&quot;.
6. L’utente aggiunge il prodotto al carrello attivando la `Cart Add` evento.
7. L’utente esegue il check-out con entrambi i prodotti.

Nel reporting, gli ordini, le entrate, le visualizzazioni dei prodotti e gli importi del carrello vengono riportati rispetto ad eVar6 e allineati all’attività del prodotto associato.

| eVar6 (metodo di ricerca dei prodotti) | ricavi | ordini | visualizzazioni di prodotto | aggiunta carrello |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| ricerca interna:camicia estiva | 19,99 | 1 | 1 | 1 |
| ricerca interna:cappello invernale | 12.99 | 1 | 1 | 1 |

Per ulteriori informazioni sull’utilizzo della sintassi della variabile di conversione, consulta la documentazione di Adobe Analytics in [implementazione di eVar utilizzando la sintassi della variabile di conversione](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

Di seguito sono riportati i campi XDM per produrre la sintassi della variabile di conversione nel tuo [!DNL Analytics] set di dati:

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`: Variabile eVar specifica a cui si accede.

#### Prodotto

```console
productListItems[#].sku
```

* `#`: Indice della matrice a cui si accede.

## Casi di utilizzo delle variabili di conversione {#conversion-variable-use-cases}

I casi d’uso riportati di seguito riflettono scenari che richiedono la sintassi della variabile di conversione.

### Eseguire un binding del valore per la coppia di prodotti ed eventi specifica

La query seguente vincola il valore alla coppia di prodotti ed eventi specifica. In questo esempio, il valore è associato all’evento di visualizzazione del prodotto.

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

La query di esempio seguente persiste il valore associato alle occorrenze successive del rispettivo prodotto. La sottoquery più bassa stabilisce la relazione del valore con il prodotto nell&#39;evento di binding dichiarato. La sottoquery successiva esegue l’attribuzione di tale valore associato nelle interazioni successive con il rispettivo prodotto. L&#39;opzione SELECT di livello superiore aggrega i risultati per produrre il reporting.

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

Leggendo questo documento, dovresti avere una migliore comprensione di come restituire un eVar di merchandising utilizzando la sintassi del prodotto e associare un valore a un prodotto specifico con la sintassi della variabile di conversione.

Se non lo hai già fatto, devi leggere il [Documentazione sulle informazioni di Analytics per le interazioni web e mobile](./analytics-insights.md) successivo. Fornisce casi d’uso comuni e illustra come utilizzare Query Service per creare informazioni fruibili dai dati Adobe Analytics web e mobili.
