---
title: Calcolo delle statistiche dei set di dati
description: In questo documento viene descritto come calcolare le statistiche a livello di colonna sui set di dati di Azure Data Lake Storage (ADLS) con comandi SQL.
source-git-commit: 02b0939ee8fe92580402a78c7ebb5a250902d01c
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Calcolo delle statistiche del set di dati

È ora possibile calcolare le statistiche a livello di colonna per [!DNL Azure Data Lake Storage] (ADLS) con `COMPUTE STATISTICS` e `SHOW STATISTICS` Comandi SQL. I comandi SQL che calcolano le statistiche dei set di dati sono un&#39;estensione del `ANALYZE TABLE` comando. Dettagli completi sulla `ANALYZE TABLE` Il comando si trova nel [Documentazione di riferimento SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Le statistiche calcolate vengono memorizzate in tabelle temporanee con persistenza a livello di sessione. Puoi accedere ai risultati dei calcoli in qualsiasi momento durante quella sessione. Non è possibile accedervi in sessioni PSQL diverse.

Per visualizzare le statistiche calcolate con `ANALYZE TABLE COMPUTE STATISTICS` è possibile utilizzare una query SELECT sul nome alias o sull&#39;ID delle statistiche. È inoltre possibile limitare l’ambito dell’analisi statistica all’intero set di dati, a un sottoinsieme di un set di dati, a tutte le colonne o a un sottoinsieme di colonne.

>[!IMPORTANT]
>
>Il `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`, e `SHOW STATISTICS` comandi non supportati nelle tabelle data warehouse. Queste estensioni per `ANALYZE TABLE` sono attualmente supportati solo per le tabelle ADLS. Per ulteriori informazioni, vedere [Sezione ANALYZE TABLE](../sql/syntax.md#analyze-table) della guida alla sintassi SQL.

Questa guida consente di strutturare le query in modo da poter calcolare le statistiche delle colonne di un set di dati ADLS. Utilizzando questi comandi, è possibile visualizzare le statistiche generate nella sessione tramite un client PSQL utilizzando una query SQL.

## Statistiche di calcolo {#compute-statistics}

Sono stati aggiunti costrutti aggiuntivi al `ANALYZE TABLE` comando che consente di: **calcolare le statistiche per un sottoinsieme di un set di dati e per determinate colonne**. Per calcolare le statistiche dei set di dati, è necessario utilizzare `ANALYZE TABLE <tableName> COMPUTE STATISTICS` formato.

>[!IMPORTANT]
>
>Il comportamento predefinito calcola le statistiche per **intero set di dati** e per **tutte le colonne**. Per calcolare le statistiche su tutte le colonne, è necessario utilizzare il formato di query `ANALYZE TABLE COMPUTE STATISTICS`. Sei **non** si consiglia di utilizzare il `COMPUTE STATISTICS` senza filtri in un set di dati ADLS, in quanto le dimensioni del set di dati possono essere molto grandi (potenzialmente petabyte di dati). In alternativa, è consigliabile eseguire sempre il comando di analisi utilizzando `FILTERCONTEXT` e un elenco specificato di colonne. Consulta le sezioni relative a [limitazione delle colonne analizzate](#limit-included-columns) e [aggiunta di una condizione di filtro](#filter-condition) per ulteriori dettagli.

L’esempio riportato di seguito calcola le statistiche per il `adc_geometric` set di dati e per **tutto** colonne nel set di dati.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>Il `COMPUTE STATISTICS` Il comando non supporta i tipi di dati array o map. È possibile impostare un `skip_stats_for_complex_datatypes` contrassegno da notificare o errore se il frame di dati di input ha colonne con array e tipi di dati mappa. Per impostazione predefinita, il flag è impostato su true. Per abilitare le notifiche o gli errori, utilizza il comando seguente: `SET skip_stats_for_complex_datatypes = false`.

## Creare un nome alias {#alias-name}

Poiché i risultati dei calcoli possono contenere una grande quantità di dati, non è ragionevole restituire i dati calcolati direttamente nell’output della console. Sebbene i nomi alias siano facoltativi, si consiglia di utilizzarli come best practice per il calcolo delle statistiche. Fornisci un nome di alias nell’istruzione per fare riferimento descrittivo ai risultati nelle query SQL. In alternativa, viene generato automaticamente `Statistics ID` viene generato e utilizzato per memorizzare le informazioni calcolate.

L’esempio seguente memorizza le statistiche calcolate di output nel `alias_name` per riferimento successivo. Il nome alias utilizzato nella query è disponibile come riferimento non appena `ANALYZE TABLE` è stato eseguito.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

L’output dell’esempio precedente è `SUCCESSFULLY COMPLETED, alias_name`. Nell&#39;output della console non vengono visualizzate le statistiche nella risposta al comando analizza statistiche di calcolo delle tabelle. Per visualizzare i risultati dettagliati, è necessario utilizzare una query SELECT sul nome alias o sull&#39;ID statistiche.

## Visualizzare l’output delle statistiche calcolate {#view-output-of-computed-statistics}

Se non si specifica in precedenza un nome di alias, Query Service genera automaticamente un nome per `Statistics ID` che segue il formato di `<tableName_stats_{incremental_number}>`. Se viene fornito un nome di alias, questo viene visualizzato nella `Statistics ID` colonna.

Esempio di output di un `COMPUTE STATISTICS` query è la seguente:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

Potrai quindi **eseguire direttamente una query sulle statistiche calcolate** facendo riferimento al `Statistics ID`. L’istruzione di esempio seguente ti consente di visualizzare l’output completo quando viene utilizzato con `Statistics ID` o il nome dell’alias.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

L’output delle statistiche calcolate potrebbe essere simile all’esempio seguente.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

## Mostra i metadati dell’analisi statistica {#show-statistics}

È possibile utilizzare `SHOW STATISTICS` per visualizzare i metadati di tutte le tabelle statistiche temporanee generate nella sessione. Questo comando consente di perfezionare l’ambito dell’analisi statistica.

Esempio di output di `SHOW STATISTICS` viene visualizzato di seguito.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Di seguito viene fornita una descrizione dei nomi delle colonne di metadati.

| Nome colonna | Descrizione |
|---|---|
| `statsId` | Questo ID fa riferimento alla tabella delle statistiche temporanee generata da `COMPUTE STATISTICS` comando. |
| `tableName` | Tabella originale utilizzata per l&#39;analisi. |
| `columnSet` | Elenco delle colonne selezionate specificamente per l&#39;analisi. Un valore vuoto indica che tutte le colonne sono state analizzate. Consulta la sezione su [limitazione delle colonne](#limit-included-columns) per ulteriori informazioni. |
| `filterContext` | Elenco dei filtri applicati all’analisi. |
| `timestamp` | Eventuali filtri cronologici applicati all’analisi dei dati per concentrarti su un periodo specifico. Consulta la [sezione condizione filtro timestamp](#filter-condition) per ulteriori dettagli. |

È possibile utilizzare l&#39;ID delle statistiche o il nome di alias per cercare le statistiche calcolate con un&#39;istruzione SELECT in qualsiasi momento all&#39;interno della sessione. L&#39;ID delle statistiche e le statistiche generate sono valide solo per questa particolare sessione e non è possibile accedervi in sessioni PSQL diverse. Le statistiche calcolate non sono al momento persistenti. Consulta la sezione su come [visualizzare l’output delle statistiche calcolate](#view-output-of-computed-statistics) per ulteriori dettagli.

## Limita le colonne incluse {#limit-included-columns}

Per concentrare l’analisi, puoi calcolare le statistiche per colonne di set di dati particolari facendo riferimento a esse per nome. Utilizza il `FOR COLUMNS (<col1>, <col2>)` sintassi per il targeting di colonne specifiche. L’esempio seguente calcola le statistiche per le colonne  `commerce`, `id`, e `timestamp` per il set di dati `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

È possibile calcolare le statistiche per qualsiasi livello principale o colonna nidificata. L&#39;esempio seguente illustra questi riferimenti.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Aggiungere una condizione filtro marca temporale {#filter-condition}

Per concentrare l’analisi delle colonne in base alla cronologia, puoi aggiungere una condizione filtro marca temporale. Questa condizione può essere utilizzata per filtrare i dati storici o concentrare l’analisi dei dati su un periodo specifico. Il `FILTERCONTEXT` Il comando calcola le statistiche su un sottoinsieme del set di dati in base alla condizione di filtro fornita.

Nell’esempio seguente, le statistiche vengono calcolate su tutte le colonne del set di dati `tableName`, in cui la marca temporale della colonna ha valori compresi tra l’intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Puoi combinare il limite di colonne e il filtro per creare query computazionali altamente specifiche per le colonne dei set di dati. Ad esempio, la query seguente calcola le statistiche sulle colonne `commerce`, `id`, e `timestamp` per il set di dati `tableName`, in cui la marca temporale della colonna ha valori compresi tra l’intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Passaggi successivi {#next-steps}

La lettura di questo documento consente di comprendere meglio come generare statistiche a livello di colonna da un set di dati ADLS utilizzando una query SQL. Si consiglia di leggere il [Guida alla sintassi SQl](../sql/syntax.md) per scoprire ulteriori funzioni di Adobe Experience Platform Query Service.
