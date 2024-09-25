---
title: Analisi dei big data efficiente con gli ipercubi in Experience Query Service
description: Scopri come utilizzare gli ipercubi in Adobe Experience Platform Query Service per ottimizzare l’analisi dei big data con un conteggio approssimativo univoco, riducendo la necessità di rielaborazione completa dei dati.
source-git-commit: e21eab682b2d29da4441a32d7307af7cf873f295
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# Analisi dei big data efficiente con ipercubi

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile solo per gli utenti che hanno acquistato lo SKU [Data Distiller](./data-distiller/overview.md). Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.

Scopri come utilizzare gli ipercubi nel servizio Experience Query di Adobe Experience Platform per eseguire analisi avanzate dei dati con una maggiore efficienza. Questo documento illustra come utilizzare le funzioni avanzate della [[!DNL Apache Datasketches] libreria](https://datasketches.apache.org/) per gestire conteggi distinti e calcoli complessi in modo incrementale, senza dover rielaborare ogni volta i dati storici.

Nell’analisi dei big data, la generazione di metriche quali conteggi distinti, quantili, elementi più frequenti, join e analisi dei grafici spesso comporta un conteggio non additivo (dove i risultati non possono essere semplicemente riassunti dai sottogruppi). I metodi tradizionali richiedono la rielaborazione di tutti i dati storici, il che può richiedere molte risorse e tempo. È possibile utilizzare gli schizzi, ovvero riepiloghi compatti che utilizzano le probabilità per rappresentare set di dati di grandi dimensioni, e funzioni avanzate di Query Service per semplificare questo processo riducendo la necessità di ricalcolare.

## Funzioni chiave degli ipercubi {#key-functions}

Gli ipercubi offrono diverse potenti funzioni per migliorare l’efficienza e la flessibilità dell’analisi dei dati.

1. **Conteggio di utenti univoci o query distinte**: utilizza le funzionalità SQL per generare conteggi univoci di utenti che interagiscono con varie dimensioni di dati, ad esempio visualizzazioni di prodotti, visite al sito o attività di e-commerce, senza rianalizzare ripetutamente i dati non elaborati.
2. **Elaborazione incrementale**: esegui aggiornamenti incrementali per piegare e unire i punti dati tra dimensioni e tempo senza ricalcolare tutto da zero.
3. **Analisi multidimensionale**: gli ipercubi consentono il filtraggio multidimensionale e la ridisposizione dei dati per creare righe di riepilogo che rappresentano combinazioni di dimensioni. Questi riepiloghi possono quindi essere utilizzati per generare informazioni con un sovraccarico di calcolo minimo.

## Casi di utilizzo per ipercubi {#use-cases}

Gli ipercubi consentono di generare in modo efficiente conteggi distinti per le varie interazioni dell’utente, senza ricalcolare ogni volta completamente i dati. Di seguito sono riportati alcuni scenari pratici per il loro utilizzo:

- Analizza i visitatori univoci che visualizzano prodotti specifici durante un periodo di tempo definito.
- Identifica gli utenti che interagiscono con più prodotti in un determinato periodo di tempo per migliorare l’analisi cross-selling.
- Puoi distinguere gli utenti che interagiscono con un prodotto ma non con un altro nel tempo, per scoprire i pattern di preferenze.
- Combina dati di interazione online e offline per ottenere una visione completa del comportamento degli utenti in un determinato periodo di tempo.
- Monitora lo spostamento degli utenti tra diverse attività all’interno di un evento per ottimizzare layout e servizi.

## Vantaggi dell&#39;utilizzo di ipercubi

In queste situazioni è possibile precalcolare le informazioni di base per categorie specifiche. Tuttavia, quando si analizzano i dati in più dimensioni e periodi di tempo, è necessario ricalcolare tutti i dati dai dati non elaborati o utilizzare un ipercubo di Query Service. Gli ipercubi semplificano il processo organizzando i dati in modo efficiente, consentendo filtri flessibili e analisi multidimensionali senza necessità di rielaborazione. Utilizzano funzioni avanzate per stimare i risultati in modo rapido e accurato e offrire vantaggi chiave quali maggiore efficienza di elaborazione, scalabilità e adattabilità per attività di analisi complesse.

### Efficienza delle dimensioni dei dati per l’elaborazione delle query

Query Service può comprimere milioni o miliardi di punti dati (ad esempio, ID utente) in un formato compatto denominato schizzo. Questo schizzo ha una dimensione dei dati significativamente ridotta per l’elaborazione delle query, che mantiene la scalabilità e rende molto più semplice e veloce l’utilizzo di. Indipendentemente dalle dimensioni dei dati originali, le dimensioni dello schizzo rimangono ridotte, il che rende l’analisi dei big data molto più gestibile ed efficiente.

Il diagramma seguente illustra come Commerce, Informazioni prodotto e Eventi ExperienceEvent delle dimensioni Web vengono elaborati in schizzi, che vengono quindi utilizzati per approssimare conteggi univoci.

![Infografica che mostra la creazione di schizzi tramite Query Service. Nel diagramma viene illustrato il modo in cui ExperienceEvents con Commerce, informazioni sul prodotto e dimensioni Web vengono elaborati in schizzi, che vengono quindi utilizzati per approssimare conteggi univoci.](./images/hypercubes/hypercube-overview.png)

### Unisci gli schizzi per rendere l’analisi dei dati più rapida e semplice

Per evitare di ricalcolare e aumentare la velocità di elaborazione, potete unire gli schizzi di categorie o gruppi diversi. Query Service semplifica inoltre la progettazione organizzando i dati in un ipercubo, dove ogni riga diventa un riepilogo della relativa partizione (una raccolta di dimensioni) insieme alla colonna di sketch. Ogni riga dell&#39;hyper-cube contiene la combinazione di dimensioni, ma non contiene dati non elaborati. Durante l’esecuzione di una query, specifica le colonne dimensionali da utilizzare per la creazione di metriche aggiuntive e unisci gli schizzi per tali righe.

![Il diagramma mostra come vengono uniti gli schizzi di diversi ExperienceEvents per creare conteggi univoci approssimativi tra le varie dimensioni.](./images/hypercubes/merge-sketches.png)

### Efficienza in termini di costi {#cost-effectiveness}

I dati dei clienti sono spesso su larga scala, ma è possibile eliminare la necessità di rielaborare i dati storici utilizzando l’elaborazione incrementale. Gli schizzi sono molto più piccoli e consentono di ottenere risultati più rapidi e in tempo reale, risparmiando allo stesso tempo sulle risorse e sui costi di elaborazione. Questa trasformazione dei dati rende le query interattive più fattibili ed efficienti.

## Panoramica delle funzioni

Questa sezione descrive come ogni funzione ottimizza l’elaborazione dei dati e migliora le capacità analitiche attraverso l’uso efficiente di schizzi e ipercubi. Descrive il loro scopo, la sintassi di esempio, i parametri e l’output previsto.

### Creare stime di conteggio univoche con gli schizzi HLL

`hll_build_agg` è una funzione di aggregazione che crea uno schizzo HLL (HyperLogLog). Questa funzione è un metodo compatto e probabilistico per stimare il numero di valori univoci all’interno di una colonna o di un’espressione in un set di dati raggruppato.

#### Definizione di funzione

```sql
hll_build_agg(column [, lgConfigK])
```

**Utilizzo:**

Nell&#39;esempio seguente viene illustrato come strutturare la funzione all&#39;interno di una query.

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Elemento “parameters”

| Parametro | Descrizione |
|---------------------------|---------------------------------------|
| `column` | Nome della colonna o della colonna in cui creare uno schizzo. |
| `lgConfigK` | *Intero* (Facoltativo) Il log-base-2 di K, dove K è il numero di bucket o slot per lo sketch HLL. Valore minimo: 4. Valore massimo: 12. Valore predefinito: 12. |

#### Output

| Colonna di output | Descrizione |
|---------------------------|---------------------------------------|
| `sketch_res` | Colonna di tipo stringa contenente lo schizzo HLL con stringhe. |

#### Esempio SQL

L&#39;esempio seguente crea uno schizzo aggregato sulla colonna `customer_id`:

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**Output di esempio SQL:**

| Paese | Schizzo |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKKCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHBAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHBAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Stimare i conteggi distinti con gli schizzi HLL

`hll_estimate` è una funzione scalare che fornisce una stima del conteggio dei valori univoci all&#39;interno di ogni riga di un set di dati. A differenza delle funzioni di aggregazione, `hll_estimate` opera in senso riga e viene utilizzato per stimare il conteggio dei valori distinti da uno schizzo all&#39;interno di singole righe.

>[!NOTE]
>
>Impossibile utilizzare questa funzione come funzione aggregata. Per i conteggi aggregati, utilizzare `sketch_count`.

#### Definizione di funzione

```sql
hll_estimate(sketch_col)
```

**Utilizzo:**

Nell&#39;esempio seguente viene illustrato come strutturare la funzione all&#39;interno di una query.

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### Elemento “parameters”

| Parametro | Descrizione |
|---------------------------|---------------------------------------|
| `sketch_column` | Colonna contenente uno schizzo HLL stratificato. Viene stimato il conteggio distinto per lo sketch in ogni riga. |

#### Output

| Colonna di output | Descrizione |
|---------------------------|---------------------------------------|
| `estimate` | Colonna di tipo double che fornisce la stima dello sketch, arrotondata a due cifre decimali. |

#### Esempio SQL

Nell&#39;esempio seguente viene stimato il conteggio distinto dei clienti per paese utilizzando la funzione `hll_estimate` in uno sketch HLL:

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**Output di esempio SQL:**

| Paese | distinct_customers_by_country |
|---------|-------------------------------|
| UA | 2,00 |
| CZ | 1,00 |
| BR | 1,00 |

### Unisci più sketch HLL con `hll_merge_agg`

`hll_merge_agg` è una funzione di aggregazione che unisce più schizzi HLL all&#39;interno di un gruppo, producendo un nuovo schizzo come output. Consente la combinazione di sketch tra partizioni o dimensioni, migliorando la flessibilità dell’analisi dei dati.

#### Definizione di funzione

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**Utilizzo:**

Nell&#39;esempio seguente viene illustrato come strutturare la funzione all&#39;interno di una query.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Elemento “parameters”

| Parametro | Descrizione |
|---------------------------|---------------------------------------|
| `sketch_column` | Colonna contenente lo schizzo HLL stratificato. |
| `allowDifferentLgConfigK` | *Booleano* (facoltativo) Se impostato su true, consente l&#39;unione di schizzi con valori `lgConfigK` diversi. Il valore predefinito è false. Viene generata un&#39;eccezione se il valore è false e gli schizzi hanno valori `lgConfigK` diversi. |

>[!NOTE]
>
>Se `allowDifferentLgConfigK` è impostato su false, l&#39;unione di schizzi con valori `lgConfigK` diversi genera un `UnsupportedOperationException`.

#### Output

| Colonna di output | Descrizione |
|----------------|-------------------------------------------------|
| `sketch_res` | Colonna di tipo sketch HLL contenente lo sketch HLL unito stratificato. |

#### Esempio SQL

Nell&#39;esempio seguente vengono uniti più schizzi HLL nella colonna `customer_id`:

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Output di esempio SQL:**

| Paese | hll_merge_agg(sketch, true) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKKKCQAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHDAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHDAMAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Stima cardinalità con `hll_merge_count_agg`

`hll_merge_count_agg` è una funzione aggregata che stima la cardinalità (numero di elementi univoci) da uno o più schizzi all&#39;interno di una colonna. Restituisce una singola stima per tutti gli schizzi rilevati all’interno del raggruppamento. Questa funzione viene utilizzata per aggregare gli schizzi e non può essere utilizzata come trasformazione per riga. Per le stime per riga, utilizzare `sketch_estimate`.

#### Definizione di funzione

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**Utilizzo:**

Nell&#39;esempio seguente viene illustrato come strutturare la funzione all&#39;interno di una query.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Elemento “parameters”

| Parametro | Descrizione |
|-------------------------|----------------------------------------------|
| `sketch_column` | Colonna contenente lo schizzo HLL stratificato. |
| `allowDifferentLgConfigK` | *Booleano* (Facoltativo) Il valore predefinito è falso. Se impostato su true, consente l&#39;unione di sketch con valori `lgConfigK` diversi. In caso contrario, viene generato un `UnsupportedOperationException`. |

#### Output

| Colonna di output | Descrizione |
|---------------|----------------------------------------------------------|
| `estimate` | Colonna di tipo Double che fornisce la stima dello sketch. |

#### Esempio SQL

Nell&#39;esempio seguente viene stimato il numero di clienti univoci con fatture utilizzando la funzione `hll_merge_count_agg`:

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**Output di esempio SQL:**

| Paese | hll_merge_count_agg(sketch, true) |
|---------|----------------------------------|
| UA | 2.0 |
| CZ | 1,0 |
| BR | 1,0 |
| MX | 2.0 |

## Limitazioni

Al momento, gli schizzi non possono essere aggiornati dopo la creazione. Aggiornamenti futuri introdurranno la funzionalità di aggiornamento degli schizzi. Grazie a questa funzionalità è possibile gestire in modo più efficace le esecuzioni senza risposta e i dati in ritardo.

## Passaggi successivi

Leggendo questo documento, ora si sa come utilizzare gli ipercubi e le funzioni di sketch associate per eseguire un&#39;elaborazione efficiente dei dati per analisi complesse e multidimensionali senza dover rielaborare i dati storici. Questo approccio consente di risparmiare tempo, ridurre i costi e offre la flessibilità necessaria per le query interattive in tempo reale, rendendola uno strumento prezioso per l’analisi di big data in Adobe Experience Platform.

Quindi, esplora altri concetti chiave come il [caricamento incrementale](./key-concepts/incremental-load.md) e la [deduplicazione dei dati](./key-concepts/deduplication.md) per comprendere meglio come utilizzare queste funzioni in modo efficace per le tue esigenze specifiche di dati.


