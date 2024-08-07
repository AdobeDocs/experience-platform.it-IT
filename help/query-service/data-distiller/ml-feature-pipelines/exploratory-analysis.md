---
title: Analisi esplorativa dei dati
description: Scopri come utilizzare Data Distiller per esplorare e analizzare i dati da un notebook Python.
exl-id: 1dd4cf6e-f7cc-4f4b-afbd-bfc1d342a2c3
source-git-commit: 27834417a1683136a173996cff1fd422305e65b9
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 13%

---

# Analisi esplorativa dei dati

In questo documento vengono forniti alcuni esempi di base e best practice per l&#39;utilizzo di Data Distiller per esplorare e analizzare i dati di un blocco appunti [!DNL Python].

## Guida introduttuva

Prima di continuare con questa guida, verificare di aver creato una connessione a Data Distiller nel blocco appunti [!DNL Python]. Per istruzioni su come [collegare un blocco appunti [!DNL Python] a Data Distiller](./establish-connection.md), vedere la documentazione.

## Acquisire statistiche di base {#basic-statistics}

Utilizza il codice seguente per recuperare il numero di righe e profili distinti in un set di dati.

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**Output di esempio**

|     | totalRows | distinctUsers |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## Creare una versione campionata di set di dati di grandi dimensioni {#create-dataset-sample}

Se il set di dati che si desidera interrogare è molto grande o se non sono necessari risultati esatti da query esplorative, utilizzare la [funzionalità di campionamento](../../key-concepts/dataset-samples.md) disponibile per le query di Data Distiller. Si tratta di un processo in due fasi:

- Innanzitutto, **analizza** il set di dati per creare una versione campionata con una proporzione di campionamento specificata
- Esegui quindi una query sulla versione campionata del set di dati. A seconda delle funzioni applicate al set di dati campionato, può essere opportuno scalare l’output in base ai numeri fino al set di dati completo

### Creare un campione del 5% {#create-sample}

L’esempio seguente analizza il set di dati e crea un campione del 5%:

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### Visualizzare gli esempi {#view-sample}

È possibile utilizzare la funzione `sample_meta` per visualizzare tutti i campioni creati da un determinato set di dati. Il frammento di codice seguente illustra come utilizzare la funzione `sample_meta`.

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**Output di esempio**:

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | tasso_di_campionamento | filter_condition_on_source_dataset | sample_num_rows | creato |
|---|---|---|---|---|---|---|---|---|
| 0 | com_summary_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | uniforme | 0,5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### Eseguire una query sull&#39;esempio {#query-sample-data}

Puoi eseguire direttamente una query sull’esempio facendo riferimento al nome della tabella di esempio dai metadati restituiti. È quindi possibile moltiplicare i risultati per il rapporto di campionamento per ottenere una stima.

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**Output di esempio**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## Analisi del funnel e-mail {#email-funnel-analysis}

Un’analisi funnel è un metodo per comprendere i passaggi necessari per raggiungere un risultato target e quanti utenti passano attraverso ciascuno di questi passaggi. L’esempio seguente illustra una semplice analisi funnel dei passaggi che conducono l’utente ad abbonarsi a una newsletter. Il risultato della sottoscrizione è rappresentato da un tipo di evento `web.formFilledOut`.

Innanzitutto, esegui una query per ottenere il numero di utenti a ogni passaggio.

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**Output di esempio**

|   | eventType | distinctUsers | distinctEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### Tracciare i risultati della query {#plot-results}

Quindi, tracciare i risultati della query utilizzando la libreria [!DNL Python] `plotly`:

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**Output di esempio**

![Infografica del funnel e-mail eventType.](../../images/data-distiller/email-funnel.png)

## Correlazioni tra eventi {#event-correlations}

Un’altra analisi comune consiste nel calcolare le correlazioni tra i tipi di evento e un tipo di evento di conversione target. In questo esempio, l&#39;evento di sottoscrizione è rappresentato da `web.formFilledOut`. In questo esempio vengono utilizzate le funzioni [!DNL Spark] disponibili nelle query di Data Distiller per eseguire i passaggi seguenti:

1. Conteggia il numero di eventi per ogni tipo di evento in base al profilo.
2. Aggregare i conteggi di ciascun tipo di evento tra i profili e calcolare le correlazioni di ciascun tipo di evento con `web,formFilledOut`.
3. Trasforma il dataframe di conteggi e correlazioni in una tabella di coefficienti di correlazione Pearson di ogni funzione (conteggi dei tipi di evento) con l’evento target.
4. Visualizzare i risultati in un plot.

Le funzioni [!DNL Spark] aggregano i dati per restituire una piccola tabella di risultati, in modo da poter eseguire questo tipo di query sull&#39;intero set di dati.

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**Output di esempio**:

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totaUsers | propositionDisplays_totalUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertisingClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDismisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | ... | 0,026805 | 0,2779 | Nessuna | 0,06014 | 0,143656 | 0,305657 | 0,218874 | 0,192836 | 0,259353 | Nessuna |

{style="table-layout:auto"}

### Trasforma riga in correlazione tipo evento {#event-type-correlation}

Quindi, trasforma la singola riga di dati nell’output della query precedente in una tabella che mostra le correlazioni di ciascun tipo di evento con l’evento di abbonamento di destinazione:

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**Output di esempio**:

|    | variabile | valore | funzionalità | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0,218874 | Aperture e-mail | 0,218874 |
| 1 | `webForms_advertisingClicks` | 0,026805 | advertisingClicks | 0,026805 |
| 2 | `webForms_productViews` | 0,277900 | productViews | 0,277900 |
| 3 | `webForms_productPurchases` | 0,000000 | productPurchases | 0,000000 |
| 4 | `webForms_propositionDismisses` | 0,060140 | propositionDismisses | 0,060140 |
| 5 | `webForms_propositionInteracts` | 0,143656 | propositionInteracts | 0,143656 |
| 6 | `webForms_emailClicks` | 0,305657 | emailClicks | 0,305657 |
| 7 | `webForms_emailOpens` | 0,218874 | emailOpens | 0,218874 |
| 8 | `webForms_emailSends` | 0,192836 | emailSends | 0,192836 |
| 9 | `webForms_webLinkClicks` | 0,259353 | webLinkClicks | 0,259353 |
| 10 | `webForms_webPageViews` | 0,000000 | webPageViews | 0,000000 |


Infine, è possibile visualizzare le correlazioni con la libreria `matplotlib` [!DNL Python]:

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![Un grafico a barre della correlazione Pearson degli eventi dei risultati dell&#39;evento](../../images/data-distiller/pearson-correlations.png)

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a utilizzare Data Distiller per esplorare e analizzare i dati di un blocco appunti [!DNL Python]. Il passaggio successivo nella creazione di pipeline di funzionalità da Experience Platform per alimentare modelli personalizzati nell&#39;ambiente di apprendimento automatico è [funzionalità di ingegneria per l&#39;apprendimento automatico](./feature-engineering.md).
