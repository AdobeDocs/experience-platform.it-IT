---
title: Calcolo delle statistiche dei set di dati
description: In questo documento viene descritto come calcolare le statistiche a livello di colonna sui set di dati di Azure Data Lake Storage (ADLS) con comandi SQL.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Calcolo delle statistiche del set di dati

È ora possibile calcolare le statistiche a livello di colonna sui set di dati [!DNL Azure Data Lake Storage] (ADLS) con il comando SQL `COMPUTE STATISTICS`. I comandi SQL che calcolano le statistiche del set di dati sono un&#39;estensione del comando `ANALYZE TABLE`. I dettagli completi sul comando `ANALYZE TABLE` sono disponibili nella [documentazione di riferimento SQL](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Le statistiche calcolate vengono memorizzate in tabelle temporanee con persistenza a livello di sessione. Puoi accedere ai risultati dei calcoli in qualsiasi momento durante quella sessione. Non è possibile accedervi in sessioni PSQL diverse.

Per visualizzare le statistiche calcolate con il comando `ANALYZE TABLE COMPUTE STATISTICS`, è possibile utilizzare una query SELECT sul nome alias o sull&#39;ID delle statistiche. È inoltre possibile limitare l’ambito dell’analisi statistica all’intero set di dati, a un sottoinsieme di un set di dati, a tutte le colonne o a un sottoinsieme di colonne.

>[!IMPORTANT]
>
>I comandi `COMPUTE STATISTICS`, `FILTERCONTEXT` e `FOR COLUMNS` non sono supportati nelle tabelle di archivio accelerate. Queste estensioni per il comando `ANALYZE TABLE` sono attualmente supportate solo per le tabelle ADLS. Per ulteriori informazioni, vedere la [sezione ANALYZE TABLE](../sql/syntax.md#analyze-table) della guida alla sintassi SQL.

Questa guida consente di strutturare le query in modo da poter calcolare le statistiche delle colonne di un set di dati ADLS. Utilizzando questi comandi, è possibile visualizzare le statistiche generate nella sessione tramite un client PSQL utilizzando una query SQL.

## Statistiche di calcolo {#compute-statistics}

Sono stati aggiunti costrutti aggiuntivi al comando `ANALYZE TABLE` che consente di **calcolare le statistiche per un sottoinsieme di un set di dati e per determinate colonne**. Per calcolare le statistiche del set di dati, è necessario utilizzare il formato `ANALYZE TABLE <tableName> COMPUTE STATISTICS`.

>[!IMPORTANT]
>
>Il comportamento predefinito calcola le statistiche per l&#39;**intero set di dati** e per **tutte le colonne**. Per calcolare le statistiche su tutte le colonne, utilizzare il formato di query `ANALYZE TABLE COMPUTE STATISTICS`. Si è **sconsigliato** utilizzare il comando `COMPUTE STATISTICS` senza filtri in un set di dati ADLS, poiché le dimensioni del set di dati possono essere molto grandi (potenzialmente petabyte di dati). In alternativa, è consigliabile eseguire sempre il comando analyze utilizzando `FILTERCONTEXT` e un elenco di colonne specificato. Per ulteriori dettagli, vedere le sezioni relative alla [limitazione delle colonne analizzate](#limit-included-columns) e all&#39;[aggiunta di una condizione di filtro](#filter-condition).

L&#39;esempio riportato di seguito calcola le statistiche per il set di dati `adc_geometric` e per **tutte** le colonne nel set di dati.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>Il comando `COMPUTE STATISTICS` non supporta i tipi di dati matrice o mappa. È possibile impostare un flag `skip_stats_for_complex_datatypes` per la notifica o per l&#39;errore se il frame di dati di input contiene colonne con matrici e tipi di dati mappa. Per impostazione predefinita, il flag è impostato su true. Per abilitare le notifiche o gli errori, utilizzare il comando seguente: `SET skip_stats_for_complex_datatypes = false`.

## Creare un nome alias {#alias-name}

Poiché i risultati dei calcoli possono contenere una grande quantità di dati, non è ragionevole restituire i dati calcolati direttamente nell’output della console. Sebbene i nomi alias siano facoltativi, si consiglia di utilizzarli come best practice per il calcolo delle statistiche. Fornisci un nome di alias nell’istruzione per fare riferimento descrittivo ai risultati nelle query SQL. In alternativa, viene generato un `Statistics ID` generato automaticamente e utilizzato per memorizzare le informazioni calcolate.

Nell&#39;esempio seguente vengono memorizzate le statistiche calcolate di output in `alias_name` per riferimento successivo. Il nome alias utilizzato nella query è disponibile come riferimento non appena viene eseguito il comando `ANALYZE TABLE`.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

L&#39;output dell&#39;esempio precedente è `SUCCESSFULLY COMPLETED, alias_name`. Nell&#39;output della console non vengono visualizzate le statistiche nella risposta al comando analizza statistiche di calcolo delle tabelle. Per visualizzare i risultati dettagliati, è necessario utilizzare una query SELECT sul nome alias o sull&#39;ID statistiche.

## Visualizzare l’output delle statistiche calcolate {#view-output-of-computed-statistics}

Se non si specifica in precedenza un nome di alias, Query Service genera automaticamente un nome per `Statistics ID` che segue il formato di `<tableName_stats_{incremental_number}>`. Se viene fornito un nome di alias, verrà visualizzato nella colonna `Statistics ID`.

Di seguito è riportato un esempio di output di una query `COMPUTE STATISTICS`:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

È quindi possibile **eseguire direttamente una query sulle statistiche calcolate** facendo riferimento a `Statistics ID`. L&#39;istruzione di esempio seguente consente di visualizzare l&#39;output completo se utilizzato con `Statistics ID` o il nome di alias.

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

È possibile utilizzare il comando `SHOW STATISTICS` per visualizzare i metadati di tutte le statistiche temporanee generate nella sessione. Questo comando consente di perfezionare l’ambito dell’analisi statistica.

Di seguito è riportato un output di esempio di `SHOW STATISTICS`.

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
| `statsId` | Questo ID fa riferimento alla tabella delle statistiche temporanee generata dal comando `COMPUTE STATISTICS`. |
| `tableName` | Tabella originale utilizzata per l&#39;analisi. |
| `columnSet` | Elenco delle colonne selezionate specificamente per l&#39;analisi. Un valore vuoto indica che tutte le colonne sono state analizzate. Per ulteriori informazioni, vedere la sezione relativa alle [colonne limite](#limit-included-columns). |
| `filterContext` | Elenco dei filtri applicati all’analisi. |
| `timestamp` | Eventuali filtri cronologici applicati all’analisi dei dati per concentrarti su un periodo specifico. Per ulteriori dettagli, consulta la sezione [condizione filtro marca temporale](#filter-condition). |

È possibile utilizzare l&#39;ID delle statistiche o il nome di alias per cercare le statistiche calcolate con un&#39;istruzione SELECT in qualsiasi momento all&#39;interno della sessione. L&#39;ID delle statistiche e le statistiche generate sono valide solo per questa particolare sessione e non è possibile accedervi in sessioni PSQL diverse. Le statistiche calcolate non sono al momento persistenti. Per ulteriori dettagli, consulta la sezione su come [visualizzare l&#39;output delle statistiche calcolate](#view-output-of-computed-statistics).

## Limita le colonne incluse {#limit-included-columns}

Per concentrare l’analisi, puoi calcolare le statistiche per colonne di set di dati particolari facendo riferimento a esse per nome. Utilizza la sintassi `FOR COLUMNS (<col1>, <col2>)` per eseguire il targeting di colonne specifiche. L&#39;esempio seguente calcola le statistiche per le colonne `commerce`, `id` e `timestamp` per il set di dati `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

È possibile calcolare le statistiche per qualsiasi livello principale o colonna nidificata. L&#39;esempio seguente illustra questi riferimenti.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Aggiungere una condizione filtro marca temporale {#filter-condition}

Per concentrare l’analisi delle colonne in base alla cronologia, puoi aggiungere una condizione filtro marca temporale. Questa condizione può essere utilizzata per filtrare i dati storici o concentrare l’analisi dei dati su un periodo specifico. Il comando `FILTERCONTEXT` calcola le statistiche su un sottoinsieme del set di dati in base alla condizione del filtro fornita.

Nell&#39;esempio seguente, le statistiche vengono calcolate su tutte le colonne per il set di dati `tableName`, dove il timestamp della colonna contiene valori compresi tra l&#39;intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Puoi combinare il limite di colonne e il filtro per creare query computazionali altamente specifiche per le colonne dei set di dati. Ad esempio, la query seguente calcola le statistiche sulle colonne `commerce`, `id` e `timestamp` per il set di dati `tableName`, dove il timestamp della colonna contiene valori compresi nell&#39;intervallo specificato di `2023-04-01 00:00:00` e `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Passaggi successivi {#next-steps}

La lettura di questo documento consente di comprendere meglio come generare statistiche a livello di colonna da un set di dati ADLS utilizzando una query SQL. Si consiglia di leggere la [guida alla sintassi SQl](../sql/syntax.md) per scoprire altre funzionalità di Adobe Experience Platform Query Service.
