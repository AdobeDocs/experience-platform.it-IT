---
keywords: Experience Platform;home;argomenti popolari;servizio query;query di esempio;query di esempio;query di esempio;adobe analytics;
solution: Experience Platform
title: Query di esempio per i dati di Adobe Analytics
description: I dati provenienti da suite di rapporti Adobe Analytics selezionate vengono trasformati in XDM ExperienceEvents e acquisiti in Adobe Experience Platform come set di dati. Questo documento delinea una serie di casi d’uso in cui Query Service utilizza questi dati e include query di esempio progettate per funzionare con i set di dati Adobe Analytics.
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Query di esempio per i dati di Adobe Analytics

I dati provenienti dalle suite di rapporti Adobe Analytics selezionate vengono trasformati in dati conformi alla [!DNL XDM ExperienceEvent] e acquisito in Adobe Experience Platform come set di dati.

Questo documento illustra una serie di casi d&#39;uso in cui Adobe Experience Platform [!DNL Query Service] utilizza questi dati. Consulta la documentazione su [Mappatura dei campi di Analytics](../../sources/connectors/adobe-applications/mapping/analytics.md) per ulteriori informazioni sulla mappatura su [!DNL Experience Events].

Consulta la sezione [documentazione del caso d’uso di analytics](../use-cases/analytics-insights.md) per scoprire come utilizzare Query Service per creare informazioni fruibili dai dati Adobe Analytics acquisiti.

## Deduplica

[!DNL Query Service] supporta la deduplicazione dei dati. Consulta la sezione [Deduplicazione dati in [!DNL Query Service] documentazione](../best-practices/deduplication.md) per informazioni su come generare nuovi valori al momento della query [!DNL Experience Event] set di dati.

## Variabili merchandising (sintassi del prodotto)

Le sezioni seguenti forniscono campi XDM e query di esempio che puoi utilizzare per accedere alle variabili di merchandising nel tuo [!DNL Analytics] set di dati.

### Sintassi del prodotto

In Adobe Analytics, i dati personalizzati a livello di prodotto possono essere raccolti attraverso variabili appositamente configurate denominate variabili merchandising. Sono basati su eventi eVar o personalizzati. La differenza tra queste variabili e il loro uso tipico è che rappresentano un valore separato per ogni prodotto trovato sull&#39;hit, anziché un solo valore per l&#39;hit.

Queste variabili sono denominate variabili di merchandising con sintassi di prodotto. Ciò consente la raccolta di informazioni, ad esempio un &quot;importo sconto&quot; per prodotto o informazioni sulla &quot;posizione sulla pagina&quot; del prodotto nei risultati di ricerca del cliente.

Per ulteriori informazioni sull’utilizzo della sintassi del prodotto, consulta la documentazione di Adobe Analytics in [implementazione di eVar utilizzando la sintassi del prodotto](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

Le sezioni seguenti descrivono i campi XDM necessari per accedere alle variabili di merchandising nel tuo [!DNL Analytics] set di dati:

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`: Indice della matrice a cui si accede.
- `evar#`: Variabile eVar specifica a cui si accede.

#### Eventi personalizzati

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`: Indice della matrice a cui si accede.
- `event#`: La variabile evento personalizzata specifica a cui si accede.

#### Query di esempio

Di seguito è riportato un esempio di query che restituisce un eVar e un evento di merchandising per il primo prodotto trovato nella `productListItems`.

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

Questa successiva query esplode la `productListItems` e restituisce ogni eVar e evento di merchandising per prodotto. La `_id` Il campo è incluso per mostrare la relazione con l’hit originale. La `_id` value è una chiave primaria univoca per il set di dati.

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
> Se tenti di recuperare un campo che non esiste nel set di dati corrente, si verificherà l’errore &quot;Nessun campo di struttura&quot;. Valuta il motivo restituito nel messaggio di errore per identificare un campo disponibile, quindi aggiorna la query ed esegui nuovamente.
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### Sintassi di conversione

Un altro tipo di variabile di merchandising trovata in Adobe Analytics è la sintassi di conversione. Con la sintassi del prodotto, il valore viene raccolto contemporaneamente al prodotto, ma ciò richiede che i dati siano presenti sulla stessa pagina. Esistono scenari in cui i dati si verificano su una pagina prima della conversione o dell’evento di interesse relativo al prodotto. Ad esempio, considerare il caso d’uso per il metodo di ricerca dei prodotti.

1. Un utente esegue e ricerca interna per &quot;cappello invernale&quot; che imposta l&#39;eVar merchandising abilitato della sintassi di conversione su &quot;ricerca interna:cappello invernale&quot;
2. L&#39;utente clicca su &quot;waffle beanie&quot; e arriva sulla pagina dei dettagli del prodotto.\
   a) L&#39;atterraggio qui si attiva via un `Product View` evento per il &quot;waffle beanie&quot; per $12.99.\
   b) Da `Product View` è configurato come evento di binding, il prodotto &quot;waffle beanie&quot; è ora associato al valore eVar6 di &quot;internal search:Winter hat&quot;. Ogni volta che viene raccolto il prodotto &quot;waffle beanie&quot;, questo verrà associato a &quot;internal search:Winter hat&quot; fino a quando (1) l&#39;impostazione di scadenza viene raggiunta o (2) viene impostato un nuovo valore eVar6 e l&#39;evento di associazione si verifica nuovamente con quel prodotto.
3. L’utente aggiunge il prodotto al carrello attivando la `Cart Add` evento.
4. L&#39;utente esegue un&#39;altra ricerca interna per &quot;camicia estiva&quot; che imposta l&#39;eVar merchandising abilitato della sintassi di conversione su &quot;ricerca interna:camicia estiva&quot;
5. L&#39;utente clicca su &quot;t-shirt sportiva&quot; e arriva sulla pagina dei dettagli del prodotto.\
   a) L&#39;atterraggio qui si attiva via un `Product View` evento per &quot;t-shirt sportiva per $19.99.\
   b) La `Product View` evento è ancora il nostro evento vincolante quindi ora il prodotto &quot;t-shirt sportiva&quot; è ora legato al valore eVar6 di &quot;ricerca interna:camicia estiva&quot; e il prodotto precedente &quot;waffle beanie&quot; è ancora legato a un valore eVar6 di &quot;ricerca interna:waffle beanie&quot;.
6. L’utente aggiunge il prodotto al carrello attivando la `Cart Add` evento.
7. L’utente esegue il check-out con entrambi i prodotti.

Nel reporting, gli ordini, le entrate, le visualizzazioni dei prodotti e gli attributi del carrello verranno riportati rispetto ad eVar6 e verranno allineati all’attività del prodotto associato.

| eVar6 (metodo di ricerca dei prodotti) | ricavi | ordini | visualizzazioni di prodotto | aggiunta carrello |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| ricerca interna:camicia estiva | 19,99 | 1 | 1 | 1 |
| ricerca interna:cappello invernale | 12.99 | 1 | 1 | 1 |

Per ulteriori informazioni sull’utilizzo della sintassi di conversione, consulta la documentazione di Adobe Analytics in [implementazione di eVar utilizzando la sintassi di conversione](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

Di seguito sono riportati i campi XDM per produrre la sintassi di conversione nel [!DNL Analytics] set di dati:

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`: Variabile eVar specifica a cui si accede.

#### Prodotto

```console
productListItems[#].sku
```

- `#`: Indice della matrice a cui si accede.

#### Query di esempio

Di seguito è riportato un esempio di query che collega il valore alla coppia di prodotti ed eventi specifica, in questo caso l’evento di visualizzazione del prodotto.

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

Ecco una query di esempio che persiste il valore associato alle occorrenze successive del rispettivo prodotto. La sottoquery più bassa stabilisce la relazione dei valori con il prodotto nell&#39;evento di binding dichiarato. La sottoquery successiva esegue l’attribuzione di tale valore associato nelle interazioni successive con il rispettivo prodotto. E il livello superiore seleziona aggrega i risultati per produrre il reporting.

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
