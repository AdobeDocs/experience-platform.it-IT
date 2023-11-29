---
title: Esempi di set di dati
description: I set di dati di esempio di Query Service consentono di eseguire query esplorative sui big data con tempi di elaborazione notevolmente ridotti a scapito della precisione delle query. Questa guida fornisce informazioni su come gestire gli esempi per l’elaborazione approssimativa delle query
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Esempi di set di dati

Adobe Experience Platform Query Service fornisce set di dati di esempio come parte delle sue funzionalità di elaborazione delle query approssimative. I set di dati di esempio vengono creati con campioni casuali uniformi da quelli esistenti [!DNL Azure Data Lake Storage] (ADLS) utilizzando solo una percentuale di record rispetto all’originale. Questa percentuale è nota come tasso di campionamento. La regolazione della frequenza di campionamento per controllare il bilanciamento tra precisione e tempo di elaborazione consente di eseguire query esplorative sui big data con tempi di elaborazione notevolmente ridotti a scapito della precisione delle query.

Poiché molti utenti non hanno bisogno di una risposta esatta per un’operazione di aggregazione su un set di dati, l’esecuzione di una query approssimativa per restituire una risposta approssimativa è più efficiente per le query esplorative su set di dati di grandi dimensioni. Poiché i set di dati di esempio contengono solo una percentuale dei dati del set di dati originale, consente di scambiare la precisione delle query per ottenere un tempo di risposta migliore. In fase di lettura, Query Service deve analizzare un numero inferiore di righe, il che produce risultati più rapidamente rispetto alle query sull’intero set di dati.

Per facilitare la gestione degli esempi per l’elaborazione approssimativa delle query, Query Service supporta le seguenti operazioni per gli esempi di set di dati:

- [Crea un esempio di set di dati casuale uniforme.](#create-a-sample)
- [Facoltativamente, specifica un criterio di filtro](##optional-filter-criteria)
- [Visualizzare l&#39;elenco dei campioni per una tabella ADLS.](#view-list-of-samples)
- [Eseguire direttamente una query sui set di dati di esempio.](#query-sample-datasets)
- [Eliminare un campione.](#delete-a-sample)
- Eliminare i campioni associati quando la tabella ADLS originale viene eliminata.

## Introduzione {#get-started}

Per utilizzare le funzionalità di elaborazione delle query approssimative di creazione ed eliminazione descritte in questo documento, è necessario impostare il flag di sessione su `true`. Dalla riga di comando dell&#39;editor di query o del client PSQL immettere `SET aqp=true;` comando.

>[!NOTE]
>
>Devi abilitare il flag di sessione ogni volta che accedi a Platform.

![Editor query con il comando SET aqp=true; evidenziato.](../images/essential-concepts/set-session-flag.png)

## Creare un esempio di set di dati casuale uniforme {#create-a-sample}

Utilizza il `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` con un nome di set di dati per creare un campione casuale uniforme da tale set di dati.

La frequenza di campionamento è la percentuale di record estratti dal set di dati originale. È possibile controllare la frequenza di campionamento utilizzando `TABLESAMPLE SAMPLERATE` parole chiave. In questo esempio, il valore di 5,0 equivale a una frequenza di campionamento del 50%. Un valore di 2,5 equivarrebbe al 25% e così via.

>[!IMPORTANT]
>
>Il sistema consente un massimo di cinque campioni per ogni set di dati. Se tenti di creare un sesto set di dati di esempio, sullo schermo viene visualizzato un messaggio di errore per informare che il limite di campioni è stato raggiunto.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Facoltativamente, specifica un criterio di filtro {#optional-filter-criteria}

È possibile scegliere di specificare un criterio di filtro per i campioni casuali uniformi. Questo consente di creare un campione basato sul sottoinsieme filtrato della tabella analizzata.

Durante la creazione di un campione, il filtro opzionale viene applicato per primo, quindi il campione viene creato dalla vista filtrata del set di dati. Un esempio di set di dati con un filtro applicato segue il seguente formato di query:

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

Di seguito sono riportati alcuni esempi pratici di questo tipo di set di dati di esempio filtrati:

```sql
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

Negli esempi forniti, il nome della tabella è `large_table`, la condizione del filtro nella tabella originale è `month(to_timestamp(timestamp)) in ('8', '9')`e la frequenza di campionamento è (X% dei dati filtrati), in questo caso `10`.

## Visualizza l’elenco degli esempi {#view-list-of-samples}

Utilizza il `sample_meta()` per visualizzare l&#39;elenco dei campioni associati a una tabella ADLS.

```sql
SELECT sample_meta('example_dataset_name')
```

L’elenco degli esempi di set di dati viene visualizzato nel formato dell’esempio seguente.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Eseguire una query sul set di dati di esempio {#query-sample-datasets}

Utilizza il `{EXAMPLE_DATASET_NAME}` per eseguire query dirette sulle tabelle di esempio. In alternativa, aggiungi `WITHAPPROXIMATE` parola chiave alla fine di una query e Query Service utilizza automaticamente l’esempio creato più di recente.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Eliminare gli esempi di set di dati {#delete-a-sample}

L’operazione di eliminazione ti consente di creare nuovi campioni una volta raggiunto il limite massimo di cinque campioni di set di dati.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Se disponi di più set di dati di esempio derivati da un set di dati ADLS originale, al momento dell’eliminazione dell’originale vengono eliminati anche tutti i campioni associati.
