---
title: Esempi di set di dati
description: I set di dati di esempio del servizio query ti consentono di eseguire query esplorative sui grandi dati con un tempo di elaborazione notevolmente ridotto al costo dell’accuratezza della query. Questa guida fornisce informazioni su come gestire i campioni per approssimare l’elaborazione delle query
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 9d543b5c7c7f39e809b6a13b8adc46b9a99f51c7
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Esempi di set di dati (rilascio limitato)

>[!IMPORTANT]
>
>La funzione di esempi di set di dati è attualmente in una versione limitata e non è disponibile per tutti i clienti.

Adobe Experience Platform Query Service fornisce set di dati di esempio come parte delle sue funzionalità di elaborazione approssimativa delle query. I set di dati di esempio vengono creati con campioni casuali uniformi provenienti da [!DNL Azure Data Lake Storage] (ADLS) set di dati che utilizzano solo una percentuale di record dell&#39;originale. Questa percentuale è nota come tasso di campionamento. La regolazione della frequenza di campionamento per controllare l&#39;equilibrio tra precisione e tempo di elaborazione consente di eseguire query esplorative sui grandi dati con tempi di elaborazione notevolmente ridotti al costo dell&#39;accuratezza della query.

Poiché molti utenti non necessitano di una risposta esatta per un’operazione di aggregazione su un set di dati, l’emissione di una query approssimativa per restituire una risposta approssimativa è più efficiente per le query esplorative su set di dati di grandi dimensioni. Poiché i set di dati di esempio contengono solo una percentuale dei dati del set di dati originale, ti consente di scambiarsi la precisione delle query per un tempo di risposta migliore. In fase di lettura, Query Service deve eseguire la scansione di un numero inferiore di righe che generano risultati più veloci rispetto a quando si desidera eseguire una query sull’intero set di dati.

Per facilitare la gestione dei campioni per l’elaborazione approssimativa delle query, Query Service supporta le seguenti operazioni per gli esempi di set di dati:

- [Crea un campione di set di dati casuale uniforme.](#create-a-sample)
- [Visualizza l&#39;elenco di campioni per una tabella ADLS.](#view-list-of-samples)
- [Esegui direttamente una query sui set di dati di esempio.](#query-sample-datasets)
- [Elimina un campione.](#delete-a-sample)
- Elimina i campioni associati quando la tabella ADLS originale viene eliminata.

## Introduzione

Per utilizzare le funzionalità di elaborazione approssimativa delle query descritte qui sopra, è necessario impostare il flag di sessione su `true`. Dalla riga di comando dell’Editor query o del client PSQL immettere il `SET aqp=true;` comando.

>[!NOTE]
>
>Devi abilitare il flag di sessione ogni volta che accedi a Platform.

![Editor query con il comando &#39;SET aqp=true;&#39; evidenziato.](../images/sql/set-session-flag.png)

## Creare un campione di set di dati casuale uniforme {#create-a-sample}

Utilizza la `ANALYZE TABLE` con un nome di set di dati per creare un campione casuale uniforme da quel set di dati.

La frequenza di campionamento è la percentuale di record prelevati dal set di dati originale. Puoi controllare la frequenza di campionamento utilizzando la variabile `TABLESAMPLE SAMPLERATE` parole chiave. In questo esempio, il valore di 5,0 equivale a una frequenza di campionamento del 50%. Un valore pari a 2,5 equivale a 25% e così via.

>[!IMPORTANT]
>
>Il sistema consente un massimo di cinque campioni per ogni set di dati. Se tenti di creare un sesto set di dati di esempio, sullo schermo viene visualizzato un messaggio di errore che indica che il limite del campione è stato raggiunto.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Visualizza l&#39;elenco dei campioni {#view-list-of-samples}

Utilizza la `sample_meta()` per visualizzare l&#39;elenco di campioni associati a una tabella ADLS.

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

## Query del set di dati di esempio {#query-sample-datasets}

Utilizza la `{EXAMPLE_DATASET_NAME}` per eseguire direttamente query sulle tabelle di esempio. In alternativa, aggiungi la `WITHAPPROXIMATE` Al termine di una query e Query Service utilizza automaticamente l&#39;esempio creato più di recente.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Elimina esempi di set di dati {#delete-a-sample}

L’operazione di eliminazione consente di creare nuovi campioni una volta raggiunto il limite massimo di cinque campioni di set di dati.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Se disponi di più set di dati di esempio derivati da un set di dati ADLS originale, quando l’originale viene rilasciato, vengono eliminati anche tutti i campioni associati.
