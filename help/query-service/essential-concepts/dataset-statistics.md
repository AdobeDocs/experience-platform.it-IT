---
title: Calcolo delle statistiche dei set di dati
description: In questo documento viene descritto come calcolare le statistiche a livello di colonna sui set di dati di Azure Data Lake Storage (ADLS) con comandi SQL.
source-git-commit: c42a7cd46f79bb144176450eafb00c2f81409380
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Calcolo delle statistiche del set di dati

È ora possibile calcolare le statistiche a livello di colonna per [!DNL Azure Data Lake Storage] (ADLS) con `COMPUTE STATISTICS` e `SHOW STATISTICS` Comandi SQL. I comandi SQL che calcolano le statistiche dei set di dati sono un&#39;estensione del `ANALYZE TABLE` comando. Dettagli completi sulla `ANALYZE TABLE` Il comando si trova nel [Documentazione di riferimento SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Attualmente, le statistiche generate sono valide solo per tale sessione e non sono persistenti tra una sessione e l’altra. Non è possibile accedervi in sessioni PSQL diverse.

Con il `SHOW STATISTICS FOR <alias_name>` , è possibile visualizzare le statistiche calcolate con il comando `ANALYZE TABLE COMPUTE STATISTICS` comando. Grazie alla combinazione di questi comandi, è ora possibile calcolare le statistiche delle colonne sull’intero set di dati, su un sottoinsieme di un set di dati, su tutte le colonne o su un sottoinsieme di colonne.

>[!IMPORTANT]
>
>Il `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, e `SHOW STATISTICS` comandi non supportati nelle tabelle data warehouse. Queste estensioni per `ANALYZE TABLE` sono attualmente supportati solo per le tabelle ADLS. Per ulteriori informazioni, vedere [Sezione ANALYZE TABLE](../sql/syntax.md#analyze-table) della guida alla sintassi SQL.

Questa guida consente di strutturare le query in modo da poter calcolare le statistiche delle colonne di un set di dati ADLS. Utilizzando questi comandi, è possibile visualizzare le statistiche generate nella sessione tramite un client PSQL utilizzando una query SQL.

## Statistiche di calcolo {#compute-statistics}

Sono stati aggiunti costrutti aggiuntivi al `ANALYZE TABLE` comando che consente di: **calcolare le statistiche per un sottoinsieme di un set di dati e per determinate colonne**. A tale scopo, è necessario utilizzare `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>Il comportamento predefinito calcola le statistiche per **intero set di dati** e per **tutte le colonne**. Per calcolare le statistiche su tutte le colonne, è necessario utilizzare il formato di query `ANALYZE TABLE COMPUTE STATISTICS`. Sei **non** si consiglia di utilizzarlo su un set di dati ADLS, in quanto le dimensioni del set di dati possono essere molto grandi (potenzialmente petabyte di dati). In alternativa, è consigliabile eseguire sempre il comando di analisi utilizzando `FILTERCONTEXT` e un elenco specificato di colonne. Consulta le sezioni relative a [limitazione delle colonne analizzate](#limit-included-columns) e [aggiunta di una condizione di filtro](#filter-condition) per ulteriori dettagli.

L’esempio riportato di seguito calcola le statistiche per il `adc_geometric` set di dati e per **tutto** colonne nel set di dati.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` non supporta i tipi di dati array o map. È possibile impostare un `skip_stats_for_complex_datatypes` contrassegno da notificare o errore se il dataframe di input ha colonne con array e tipi di dati mappa. Per impostazione predefinita, il flag è impostato su true. Per abilitare le notifiche o gli errori, utilizza il comando seguente: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

L&#39;output della console non visualizza le statistiche in risposta al comando di analisi delle statistiche di calcolo delle tabelle. Nella console verrà invece visualizzata una singola colonna di righe di `Statistics ID` con un identificatore univoco universale per fare riferimento ai risultati. Al completamento di un `COMPUTE STATISTICS` query, i risultati vengono visualizzati come segue:

```console
| Statistics ID    | 
| ---------------- |
| QqMtDfHQOdYJpZlb |
(1 row)
```

Per visualizzare l’output, utilizza `SHOW STATISTICS` comando. Istruzioni su [come visualizzare le statistiche](#show-statistics) vengono fornite più avanti nel documento.

## Limita le colonne incluse {#limit-included-columns}

È possibile calcolare le statistiche per determinate colonne di set di dati facendo riferimento ad esse per nome. Utilizza il `FOR COLUMNS (<col1>, <col2>)` sintassi per il targeting di colonne specifiche. L’esempio seguente calcola le statistiche per le colonne  `commerce`, `id`, e `timestamp` per il set di dati `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

È possibile calcolare le statistiche per qualsiasi livello principale o colonna nidificata. L&#39;esempio seguente illustra questi riferimenti.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Aggiungere una condizione filtro marca temporale {#filter-condition}

Puoi aggiungere una condizione di filtro per la marca temporale per concentrare l’analisi delle colonne. Può essere utilizzato per filtrare i dati storici o concentrare l’analisi dei dati su un periodo specifico. Il `FILTERCONTEXT` Il comando calcola le statistiche su un sottoinsieme del set di dati in base alla condizione di filtro fornita.

Nell’esempio seguente, le statistiche vengono calcolate su tutte le colonne del set di dati `tableName`, in cui la marca temporale della colonna ha valori compresi tra l’intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Puoi combinare il limite di colonne e il filtro per creare query computazionali altamente specifiche per le colonne dei set di dati. Ad esempio, la query seguente calcola le statistiche sulle colonne `commerce`, `id`, e `timestamp` per il set di dati `tableName`, in cui la marca temporale della colonna ha valori compresi tra l’intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- ## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. -->

## Mostra le statistiche {#show-statistics}

<!-- Commented out until the <alias_name> feature is released.
The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  -->

Anche con una condizione di filtro e un elenco di colonne, il calcolo può eseguire il targeting di una grande quantità di dati. Query Service genera un identificatore univoco universale per l’ID delle statistiche per memorizzare le informazioni calcolate. Puoi quindi utilizzare questo ID di statistiche per cercare le statistiche calcolate con `SHOW STATISTICS` in qualsiasi momento della sessione.

L&#39;ID delle statistiche e le statistiche generate sono valide solo per questa particolare sessione e non è possibile accedervi in sessioni PSQL diverse. Le statistiche calcolate non sono al momento persistenti. Per visualizzare le statistiche, utilizza il comando illustrato di seguito.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

Un output potrebbe essere simile all’esempio seguente.

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

## Passaggi successivi {#next-steps}

La lettura di questo documento consente di comprendere meglio come generare statistiche a livello di colonna da un set di dati ADLS utilizzando una query SQL. Si consiglia di leggere il [Guida alla sintassi SQl](../sql/syntax.md) per scoprire ulteriori funzioni di Adobe Experience Platform Query Service.
