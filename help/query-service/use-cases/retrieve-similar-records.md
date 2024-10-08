---
title: Recuperare record simili con funzioni di ordine superiore
description: Scopri come identificare e recuperare record simili o correlati da uno o più set di dati in base a una metrica di somiglianza e a una soglia di somiglianza. Questo flusso di lavoro può evidenziare relazioni significative o sovrapposizioni tra set di dati diversi.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# Recuperare record simili con funzioni di ordine superiore

Utilizza le funzioni di ordine superiore di Data Distiller per risolvere una serie di casi d’uso comuni. Per identificare e recuperare record simili o correlati da uno o più set di dati, utilizza le funzioni di filtro, trasformazione e riduzione descritte in questa guida. Per informazioni su come utilizzare le funzioni di ordine superiore per elaborare tipi di dati complessi, vedere la documentazione su come [gestire tipi di dati array e mappa](../sql/higher-order-functions.md).

Utilizza questa guida per identificare prodotti da set di dati diversi che hanno una somiglianza significativa nelle loro caratteristiche o attributi. Questa metodologia fornisce soluzioni per: deduplicazione dei dati, collegamento dei record, sistemi di consigli, recupero delle informazioni e analisi testuale, tra gli altri.

Il documento descrive il processo di implementazione di un similarity join, che utilizza quindi funzioni di ordine superiore di Data Distiller per calcolare la somiglianza tra set di dati e filtrarli in base agli attributi selezionati. Vengono forniti snippet di codice SQL e spiegazioni per ogni passaggio del processo. Il flusso di lavoro implementa join di somiglianza utilizzando la misura di somiglianza Jaccard e la tokenizzazione utilizzando le funzioni di ordine superiore di Data Distiller. Questi metodi vengono quindi utilizzati per identificare e recuperare record simili o correlati da uno o più set di dati in base a una metrica di somiglianza. Le sezioni chiave del processo includono: [tokenizzazione utilizzando funzioni di ordine superiore](#data-transformation), [cross-join di elementi univoci](#cross-join-unique-elements), [calcolo della somiglianza Jaccard](#compute-the-jaccard-similarity-measure) e [filtro basato su soglia](#similarity-threshold-filter).

## Prerequisiti

Prima di continuare con questo documento, è necessario conoscere i concetti seguenti:

- Un **similarity join** è un&#39;operazione che identifica e recupera coppie di record da una o più tabelle in base a una misura di somiglianza tra i record. I requisiti chiave per un join per similarità sono i seguenti:
   - **Metrica di similarità**: un join per similarità si basa su una metrica o misura di similarità predefinita. Tali metriche includono: somiglianza Jaccard, somiglianza coseno, distanza di modifica e così via. La metrica dipende dalla natura dei dati e dal caso d’uso. Questa metrica quantifica la somiglianza o la diversità di due record.
   - **Soglia**: viene utilizzata una soglia di somiglianza per determinare quando i due record sono considerati abbastanza simili da essere inclusi nel risultato del join. I record con un punteggio di somiglianza superiore alla soglia vengono considerati corrispondenze.
- L&#39;indice di somiglianza **Jaccard**, o misura di somiglianza Jaccard, è una statistica utilizzata per misurare la somiglianza e la diversità dei set di campioni. Viene definita come la dimensione dell&#39;intersezione divisa per la dimensione dell&#39;unione dei set di campioni. La misurazione della somiglianza Jaccard è compresa tra zero e uno. Una somiglianza Jaccard pari a zero indica nessuna somiglianza tra i set e una somiglianza Jaccard pari a uno indica che i set sono identici.
  ![Un diagramma di Venn per illustrare la misurazione della somiglianza Jaccard.](../images/use-cases/jaccard-similarity.png)
- **Le funzioni di ordine superiore** in Data Distiller sono strumenti dinamici e inline che elaborano e trasformano i dati direttamente all&#39;interno delle istruzioni SQL. Queste funzioni versatili eliminano la necessità di più passaggi nella manipolazione dei dati, in particolare quando [si occupa di tipi complessi come array e mappe](../sql/higher-order-functions.md). Migliorando l’efficienza delle query e semplificando le trasformazioni, le funzioni di ordine più elevato contribuiscono a rendere più agili le analisi e a migliorare il processo decisionale in vari scenari aziendali.

## Introduzione

Lo SKU di Data Distiller è necessario per eseguire le funzioni di ordine superiore sui dati Adobe Experience Platform. Se non disponi dello SKU di Data Distiller, contatta il rappresentante dell’assistenza clienti Adobe per ulteriori informazioni.

## Stabilisci somiglianza {#establish-similarity}

Questo caso d’uso richiede una misura di somiglianza tra stringhe di testo che può essere utilizzata in un secondo momento per stabilire una soglia per il filtro. In questo esempio, i prodotti degli insiemi A e B rappresentano le parole di due documenti.

La misura di somiglianza Jaccard può essere applicata a un&#39;ampia gamma di tipi di dati, inclusi dati di testo, dati categorici e dati binari. È inoltre adatto all’elaborazione in tempo reale o in batch, in quanto può essere computazionalmente efficiente da calcolare per set di dati di grandi dimensioni.

I set di prodotti A e B contengono i dati di test per questo flusso di lavoro.

- Set di prodotti A: `{iPhone, iPad, iWatch, iPad Mini}`
- Set di prodotti B: `{iPhone, iPad, Macbook Pro}`

Per calcolare la somiglianza Jaccard tra i set di prodotti A e B, trovare innanzitutto l&#39;**intersezione** (elementi comuni) dei set di prodotti. In questo caso, `{iPhone, iPad}`. Quindi, trova la **unione** (tutti gli elementi univoci) di entrambi i set di prodotti. In questo esempio, `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Infine, utilizzare la formula di somiglianza Jaccard: `J(A,B) = A∪B / A∩B` per calcolare la somiglianza.

J = Distanza jaccard
A = set 1
B = insieme 2

La somiglianza Jaccard tra i set di prodotti A e B è 0,4. Ciò indica un moderato grado di somiglianza tra le parole utilizzate nei due documenti. Questa somiglianza tra i due set definisce le colonne nell&#39;unione di somiglianza. Queste colonne rappresentano informazioni, o caratteristiche associate ai dati, memorizzate in una tabella e utilizzate per eseguire i calcoli di similarità.

### Calcolo Jaccard a coppie con somiglianza stringa {#pairwise-similarity}

Per confrontare in modo più preciso le somiglianze tra stringhe, è necessario calcolare la somiglianza a coppie. La somiglianza a coppie divide gli oggetti altamente dimensionali in oggetti dimensionali più piccoli per il confronto e l&#39;analisi. A questo scopo, una stringa di testo viene suddivisa in parti o unità (token) più piccole. Potrebbero essere singole lettere, gruppi di lettere (come le sillabe) o intere parole. La somiglianza viene calcolata per ogni coppia di token tra ciascun elemento dell&#39;insieme A e ciascun elemento dell&#39;insieme B. Questa tokenizzazione fornisce una base per confronti analitici e computazionali, relazioni e informazioni da trarre dai dati.

Per il calcolo della somiglianza a coppie, in questo esempio vengono utilizzati due grammi di caratteri (token di due caratteri) per confrontare una corrispondenza di somiglianza tra le stringhe di testo dei prodotti negli insiemi A e B. Un bi-grammo è una sequenza consecutiva di due elementi o elementi in una determinata sequenza o testo. Puoi generalizzarlo in n grammi.

Questo esempio presuppone che il caso non abbia importanza e che gli spazi non debbano essere presi in considerazione. In base a questi criteri, gli insiemi A e B hanno i seguenti bi-grammi:

Set di prodotti A:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Set di prodotti B bi-grammi:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Quindi, calcola il coefficiente di somiglianza Jaccard per ogni coppia:

|                   | iPhone (Set B) | iPad (Set B) | Macbook Pro (Set B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Set A) | (Intersezione: 5, Unione: 5) = 5 / 5 = 1 | (Intersezione: 1, Unione: 7) =1 / 7 ≈ 0,14 | (Intersezione: 0, Unione: 14) = 0 / 14 = 0 |
| iPad (Set A) | (Intersezione: 1, Unione: 7) = 1 / 7 ≈ 0,14 | (Intersezione: 3, Unione: 3) = 3 / 3 = 1 | (Intersezione: 0, Unione: 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Intersezione: 0, Unione: 8) = 0 / 8 = 0 | (Intersezione: 0, Unione: 8) = 0 / 8 = 0 | (Intersezione: 0, Unione: 8) = 0 / 8 =0 |
| iPad Mini (Set A) | (Intersezione: 1, Unione: 11) = 1 / 11 ≈ 0,09 | (Intersezione: 3, Unione: 7) = 3 / 7 ≈ 0,43 | (Intersezione: 0, Unione: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Creare i dati di test con SQL {#create-test-data}

Per creare manualmente una tabella di test per i set di prodotti, utilizzare l&#39;istruzione SQL CREATE TABLE.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

Le descrizioni seguenti forniscono un raggruppamento del blocco di codice SQL precedente:

- Riga 1: `CREATE TEMP TABLE featurevector1 AS`: questa istruzione crea una tabella temporanea denominata `featurevector1`. Le tabelle temporanee sono in genere accessibili solo all&#39;interno della sessione corrente e vengono eliminate automaticamente alla fine della sessione.
- Riga 1 e 2: `SELECT * FROM (...)`: questa parte del codice è una sottoquery utilizzata per generare i dati inseriti nella tabella `featurevector1`.
All&#39;interno della sottoquery, più istruzioni `SELECT` vengono combinate utilizzando il comando `UNION ALL`. Ogni istruzione `SELECT` genera una riga di dati con i valori specificati per la colonna `ProductName`.
- Riga 3: `SELECT 'iPad' AS ProductName`: viene generata una riga con il valore `iPad` nella colonna `ProductName`.
- Riga 5: `SELECT 'iPhone'`: genera una riga con il valore `iPhone` nella colonna `ProductName`.

L&#39;istruzione SQL crea una tabella come illustrato di seguito:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Per creare il secondo vettore di funzionalità, utilizzare l&#39;istruzione SQL seguente:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Trasformazioni dati {#data-transformation}

In questo esempio, è necessario eseguire diverse azioni per confrontare accuratamente i set. In primo luogo, gli spazi vuoti vengono rimossi dai vettori di feature poiché si presume che non contribuiscano alla misura di similarità. Quindi, eventuali duplicati presenti nel vettore della funzione vengono rimossi poiché sprecano l’elaborazione computazionale. Successivamente, i token di due caratteri (bi-grammi) vengono estratti dai vettori della funzione. In questo esempio, si presume che si sovrappongano.

>[!NOTE]
>
>A scopo illustrativo, le colonne elaborate vengono aggiunte accanto al vettore di funzione per ciascuno dei passaggi.

Le sezioni seguenti illustrano le trasformazioni di dati preliminari come la deduplicazione, la rimozione degli spazi vuoti e la conversione in minuscolo prima di avviare il processo di tokenizzazione.

### Deduplica {#deduplication}

Utilizzare quindi la clausola `DISTINCT` per rimuovere i duplicati. In questo esempio non ci sono duplicati, ma è un passo importante per migliorare la precisione di qualsiasi confronto. Di seguito viene visualizzato il codice SQL necessario:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Rimozione spazio vuoto {#whitespace-removal}

Nell&#39;istruzione SQL seguente, gli spazi vuoti vengono rimossi dai vettori di funzionalità. La parte `replace(ProductName, ' ', '') AS featurevector1_nospaces` della query prende la colonna `ProductName` dalla tabella `featurevector1` e utilizza la funzione `replace()`. La funzione `REPLACE` sostituisce tutte le occorrenze di uno spazio (&#39; &#39;) con una stringa vuota (&#39;&#39;). Rimuove tutti gli spazi dai valori `ProductName`. Il risultato è impostato come `featurevector1_nospaces`.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

I risultati sono riportati nella tabella seguente:

|   | feature vector1_distinct | feature vector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Di seguito sono riportati l&#39;istruzione SQL e i relativi risultati sul secondo vettore di funzionalità:

+++Seleziona per espandere

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

I risultati vengono visualizzati come segue:

|   | feature vector2_distinct | feature vector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Converti in minuscolo {#lowercase-conversion}

L’istruzione SQL viene quindi migliorata per convertire i nomi dei prodotti in minuscolo e rimuovere eventuali spazi vuoti. La funzione più bassa (`lower(...)`) viene applicata al risultato della funzione `replace()`. La funzione lower converte tutti i caratteri nei valori `ProductName` modificati in minuscolo. In questo modo i valori vengono scritti in minuscolo, indipendentemente dalle lettere maiuscole e minuscole originali.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Il risultato di questa istruzione è:

|   | feature vector1_distinct | feature vector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Di seguito sono riportati l&#39;istruzione SQL e i relativi risultati sul secondo vettore di funzionalità:

+++Seleziona per espandere

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

I risultati vengono visualizzati come segue:

|   | feature vector2_distinct | feature vector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Estrarre i token utilizzando SQL {#tokenization}

Il passaggio successivo è la tokenizzazione o la suddivisione del testo. La token è il processo che consiste nel prendere il testo e suddividerlo in singoli termini. In genere questo comporta la suddivisione delle frasi in parole. In questo esempio, le stringhe vengono suddivise in bi-grammi (e n-grammi di ordine superiore) estraendo i token utilizzando funzioni SQL come `regexp_extract_all`. Per una tokenizzazione efficace è necessario generare due grammi sovrapposti.

L&#39;istruzione SQL è stata ulteriormente migliorata per utilizzare `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Questa parte della query elabora ulteriormente i valori `ProductName` modificati creati nel passaggio precedente. Utilizza la funzione `regexp_extract_all()` per estrarre tutte le sottostringhe non sovrapposte di uno o due caratteri dai valori `ProductName` modificati e minuscoli. Il modello di espressione regolare `.{2}` corrisponde a sottostringhe di due caratteri in lunghezza. La parte `regexp_extract_all(..., '.{2}', 0)` della funzione estrae quindi tutte le sottostringhe corrispondenti dal testo di input.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector1_distinct | feature vector1_transform | token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Per migliorare ulteriormente la precisione, è necessario utilizzare l’istruzione SQL per creare token sovrapposti. Ad esempio, nella stringa &quot;iPad&quot; precedente manca il token &quot;pa&quot;. Per risolvere questo problema, spostare l&#39;operatore lookahead (utilizzando `substring`) di un passaggio e generare i bi-grammi.

Analogamente al passaggio precedente, `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` estrae sequenze di due caratteri dal nome del prodotto modificato, ma inizia dal secondo carattere utilizzando il metodo `substring` per creare token sovrapposti. Successivamente, nelle righe da 3 a 7 (`array_union(...) AS tokens`), la funzione `array_union()` combina le matrici di sequenze di due caratteri ottenute dalle due estrazioni di espressioni regolari. In questo modo il risultato contiene token univoci sia per le sequenze non sovrapposte che per quelle sovrapposte.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector1_distinct | feature vector1_transform | token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Tuttavia, l&#39;utilizzo di `substring` come soluzione al problema presenta delle limitazioni. Se si dovessero creare token dal testo in base a tre grammi (tre caratteri), occorrerebbe utilizzare due `substrings` per guardare avanti due volte per ottenere i turni richiesti. Per fare 10 grammi, sono necessarie nove espressioni `substring`. In questo modo il codice si gonfia e diventa insostenibile. L’utilizzo di espressioni regolari semplici non è appropriato. Occorre un nuovo approccio.

### Regola per la lunghezza del nome del prodotto {#length-adjustment}

La funzione SQl può essere migliorata con le funzioni di sequenza e lunghezza. Nell&#39;esempio seguente, `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` genera una sequenza di numeri da uno alla lunghezza del nome del prodotto modificato meno tre. Ad esempio, se il nome del prodotto modificato è &quot;ipadmini&quot; con una lunghezza di otto caratteri, vengono generati numeri da uno a cinque (otto-tre).

L’istruzione seguente estrae nomi di prodotto univoci e suddivide ogni nome in sequenze di caratteri (token) di quattro lunghezze di caratteri, esclusi gli spazi, e li presenta come due colonne. Una colonna mostra i nomi di prodotto univoci e l’altra colonna mostra i token generati.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector1_distinct | token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### Assicurati di impostare la lunghezza del token {#ensure-set-token-length}

È possibile aggiungere ulteriori condizioni all’istruzione per garantire che le sequenze generate abbiano una lunghezza specifica. L&#39;istruzione SQL seguente espande la logica di generazione del token rendendo più complessa la funzione `transform`. L&#39;istruzione utilizza la funzione `filter` all&#39;interno di `transform` per garantire che le sequenze generate abbiano una lunghezza di sei caratteri. Gestisce i casi in cui ciò non sia possibile assegnando valori NULL a tali posizioni.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector1_distinct | token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Esplora le soluzioni utilizzando le funzioni di ordine superiore di Data Distiller {#higher-order-function-solutions}

Le funzioni di ordine superiore sono costrutti potenti che consentono di implementare una &quot;programmazione&quot; simile alla sintassi in Data Distiller. Possono essere utilizzati per iterare una funzione su più valori in un array.

Nel contesto di Data Distiller, le funzioni di ordine superiore sono ideali per la creazione di n-grammi e per l’iterazione su sequenze di caratteri.

La funzione `reduce`, in particolare se utilizzata all&#39;interno di sequenze generate da `transform`, consente di derivare valori cumulativi o aggregati, che possono essere fondamentali in vari processi di analisi e pianificazione.

Ad esempio, nell&#39;istruzione SQl seguente, la funzione `reduce()` aggrega gli elementi in un array utilizzando un aggregatore personalizzato. Simula un ciclo for per **creare le somme cumulative di tutti i numeri interi** da uno a cinque. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

Di seguito è riportata un&#39;analisi dell&#39;istruzione SQL:

- Riga 1: `transform` applica la funzione `x -> reduce` su ogni elemento generato nella sequenza.
- Riga 2: `sequence(1, 5)` genera una sequenza di numeri da uno a cinque.
- Riga 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` esegue un&#39;operazione di riduzione per ogni elemento x nella sequenza (da 1 a 5).
   - La funzione `reduce` richiede un valore di accumulo iniziale pari a 0, una sequenza da uno al valore corrente di `x` e una funzione di ordine superiore `(acc, y) -> acc + y` per aggiungere i numeri.
   - La funzione di ordine superiore `acc + y` accumula la somma aggiungendo il valore corrente `y` all&#39;accumulatore `acc`.
- Riga 8: `AS sum_result` rinomina la colonna risultante come sum_result.

In sintesi, questa funzione di ordine superiore accetta due parametri (`acc` e `y`) e definisce l&#39;operazione da eseguire, che in questo caso sta aggiungendo `y` all&#39;accumulatore `acc`. Questa funzione di ordine superiore viene eseguita per ogni elemento della sequenza durante il processo di riduzione.

L&#39;output di questa istruzione è una singola colonna (`sum_result`) contenente le somme cumulative di numeri da uno a cinque.

### Il valore delle funzioni di ordine superiore {#value-of-higher-order-functions}

Questa sezione analizza una versione ridotta di un&#39;istruzione SQL a tre grammi per comprendere meglio il valore delle funzioni di ordine superiore in Data Distiller e creare n grammi in modo più efficiente.

L&#39;istruzione seguente funziona sulla colonna `ProductName` nella tabella `featurevector1`. Genera un set di sottostringhe di tre caratteri derivate dai nomi dei prodotti modificati all’interno della tabella, utilizzando le posizioni ottenute dalla sequenza generata.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Di seguito è riportata un&#39;analisi dell&#39;istruzione SQL:

- Riga 2: `transform` applica una funzione di ordine superiore a ogni numero intero della sequenza.
- Riga 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` genera una sequenza di numeri interi compresi tra `1` e la lunghezza del nome del prodotto modificato meno due.
   - `length(lower(replace(ProductName, ' ', '')))` calcola la lunghezza di `ProductName` dopo averlo convertito in minuscolo e aver rimosso gli spazi.
   - `- 2` sottrae due dalla lunghezza per garantire che la sequenza generi posizioni di partenza valide per le sottostringhe di 3 caratteri. Sottraendo 2 si ottiene un numero di caratteri sufficiente dopo ogni posizione iniziale per estrarre una sottostringa di 3 caratteri. La funzione di sottostringa qui funziona come un operatore lookahead.
- Riga 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` è una funzione di ordine superiore che opera su ogni numero intero `i` nella sequenza generata.
   - La funzione `substring(...)` estrae una sottostringa di 3 caratteri dalla colonna `ProductName`.
   - Prima di estrarre la sottostringa, `lower(replace(ProductName, ' ', ''))` converte `ProductName` in minuscolo e rimuove gli spazi per garantire la coerenza.

L’output è un elenco di sottostringhe di tre caratteri di lunghezza, estratte dai nomi dei prodotti modificati, in base alle posizioni specificate nella sequenza.

## Filtrare i risultati {#filter-results}

La funzione `filter`, con le successive [trasformazioni di dati](#data-transformation), consente un&#39;estrazione più precisa e precisa delle informazioni rilevanti dai dati di testo. Questo consente di ottenere informazioni approfondite, migliorare la qualità dei dati e facilitare processi decisionali migliori.

La funzione `filter` nell&#39;istruzione SQL seguente consente di perfezionare e limitare la sequenza di posizioni all&#39;interno della stringa da cui vengono estratte le sottostringhe utilizzando la funzione di trasformazione successiva.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

La funzione `filter` genera una sequenza di posizioni iniziali valide all&#39;interno del `ProductName` modificato ed estrae sottostringhe di una lunghezza specifica. Sono consentite solo le posizioni iniziali che consentono l’estrazione di una sottostringa di sette caratteri.

La condizione `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` assicura che la posizione iniziale `i` più `6` (la lunghezza della sottostringa di sette caratteri desiderata meno uno) non superi la lunghezza del `ProductName` modificato.

L&#39;istruzione `CASE` viene utilizzata per includere o escludere in modo condizionale le sottostringhe in base alla lunghezza. Sono incluse solo le sottostringhe di sette caratteri; le altre sono sostituite da NULL. Queste sottostringhe vengono quindi utilizzate dalla funzione `transform` per creare una sequenza di sottostringhe dalla colonna `ProductName` nella tabella `featurevector1`.

>[!TIP]
>
>Puoi utilizzare la funzione [modelli con parametri](../ui/parameterized-queries.md) per riutilizzare e astrarre la logica all&#39;interno delle query. Ad esempio, quando si creano funzioni di utilità generiche (come quella visualizzata sopra per le stringhe di tokenizzazione), è possibile utilizzare i modelli con parametri di Data Distiller in cui il numero di caratteri sarebbe un parametro.

## Calcola la cross-join di elementi univoci tra due vettori di funzionalità {#cross-join-unique-elements}

L’identificazione delle differenze o delle discrepanze tra i due set di dati in base a una trasformazione specifica dei dati è un processo comune per mantenere l’accuratezza dei dati, migliorarne la qualità e garantire la coerenza tra i diversi set di dati.

L&#39;istruzione SQL seguente estrae i nomi di prodotto univoci presenti in `featurevector2` ma non in `featurevector1` dopo l&#39;applicazione delle trasformazioni.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Oltre a `EXCEPT`, puoi anche utilizzare `UNION` e `INTERSECT` a seconda del caso d&#39;uso. Inoltre, è possibile sperimentare con le clausole `ALL` o `DISTINCT` per vedere la differenza tra l&#39;inclusione di tutti i valori e la restituzione solo dei valori univoci per le colonne specificate.

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | lower(replace(ProductName, &#39; &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Quindi, eseguite un cross join per combinare gli elementi dei due vettori di feature per creare coppie di elementi da confrontare. Il primo passo in questo processo è la creazione di un vettore tokenizzato.

Un vettore tokenizzato è una rappresentazione strutturata di dati di testo in cui ogni parola, frase o unità di significato (token) viene convertito in un formato numerico. Questa conversione consente agli algoritmi di elaborazione del linguaggio naturale di comprendere e analizzare le informazioni testuali.

La SQl seguente crea un vettore tokenizzato.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Se si utilizza [!DNL DbVisualizer], dopo aver creato o eliminato una tabella, aggiornare la connessione al database in modo da aggiornare la cache dei metadati della tabella. Data Distiller non invia aggiornamenti dei metadati.

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector1_distinct | token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Quindi ripetere il processo per `featurevector2`:

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

|   | feature vector2_distinct | token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Con entrambi i vettori tokenizzati completati, ora puoi creare il cross join. Questo è visibile nelle istruzioni SQL seguenti:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Di seguito è riportato un riepilogo dei valori SQl utilizzati per creare il cross join:

- Riga 2: `A.featurevector1_distinct AS SetA_ProductNames` seleziona la colonna `featurevector1_distinct` dalla tabella `A` e le assegna un alias `SetA_ProductNames`. Questa sezione di SQL genera un elenco di nomi di prodotto distinti dal primo set di dati.
- Riga 4: `A.tokens AS SetA_tokens1` seleziona la colonna `tokens` dalla tabella o dalla sottoquery `A` e le assegna un alias `SetA_tokens1`. Questa sezione di SQL genera un elenco di valori tokenizzati associati ai nomi dei prodotti del primo set di dati.
- Riga 8: l&#39;operazione `CROSS JOIN` combina tutte le possibili combinazioni di righe dei due set di dati. In altre parole, ogni nome di prodotto e i token associati della prima tabella (`A`) vengono associati a ogni nome di prodotto e ai token associati della seconda tabella (`B`). Questo determina un prodotto cartesiano dei due set di dati, in cui ogni riga nell’output rappresenta una combinazione di un nome di prodotto e dei relativi token associati da entrambi i set di dati.

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

| * | SetA_ProductName | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Calcola la misura di somiglianza Jaccard {#compute-the-jaccard-similarity-measure}

Quindi, calcola utilizzando il coefficiente di somiglianza Jaccard per eseguire un&#39;analisi di somiglianza tra i due set di nomi di prodotto confrontando le loro rappresentazioni tokenizzate. L’output dello script SQL seguente fornisce quanto segue: nomi di prodotto da entrambi i set, le loro rappresentazioni tokenizzate, conteggi di token univoci comuni e totali e il coefficiente di somiglianza Jaccard calcolato per ogni coppia di set di dati.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Di seguito è riportato un riepilogo del codice SQL utilizzato per calcolare il coefficiente di somiglianza Jaccard:

- Riga 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` calcola il numero di token comuni a `SetA_tokens1` e `SetB_tokens2`. Questo calcolo si ottiene calcolando la dimensione dell&#39;intersezione dei due array di token.
- Riga 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` calcola il numero totale di token univoci sia per `SetA_tokens1` che per `SetB_tokens2`. Questa riga calcola la dimensione dell’unione dei due array di token.
- Riga 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` calcola la somiglianza Jaccard tra i set di token. Queste righe dividono la dimensione dell’intersezione del token per la dimensione dell’unione dei token e arrotondano il risultato a due posizioni decimali. Il risultato è un valore compreso tra zero e uno, dove uno indica una completa somiglianza.

I risultati sono riportati nella tabella seguente:

+++Seleziona per espandere

| * | SetA_ProductName | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Somiglianza jaccard |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1,0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1,0 |

{style="table-layout:auto"}

+++

## Filtra i risultati in base alla soglia di somiglianza Jaccard {#similarity-threshold-filter}

Infine, filtra i risultati in base a una soglia predefinita per selezionare solo le coppie che soddisfano i criteri di somiglianza. L’istruzione SQL seguente filtra i prodotti con un coefficiente di somiglianza Jaccard di almeno 0,4. Questo limita i risultati a coppie che mostrano un notevole grado di somiglianza.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

I risultati di questa query forniscono le colonne per l&#39;unione per similarità, come illustrato di seguito:

+++Seleziona per espandere

|   | SetA_ProductName | SetA_ProductName |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Passaggi successivi {#next-steps}

Leggendo questo documento, ora puoi utilizzare questa logica per evidenziare relazioni significative o sovrapposizioni tra set di dati diversi. La capacità di identificare prodotti da diversi set di dati che hanno una somiglianza significativa nelle loro caratteristiche o attributi ha numerose applicazioni nel mondo reale. Questa logica può essere utilizzata per scenari quali:

- Corrispondenza prodotto: per raggruppare o consigliare prodotti simili ai clienti.
- Pulizia dei dati: per migliorare la qualità dei dati.
- Analisi del paniere di mercato: per fornire informazioni sul comportamento dei clienti, sulle preferenze e sulle potenziali opportunità di cross-selling.

Se non lo hai già fatto, ti consigliamo di leggere la [panoramica sulla pipeline delle funzionalità AI/ML](../data-distiller/ml-feature-pipelines/overview.md). Utilizza questa panoramica per scoprire come Data Distiller e l’apprendimento automatico che preferisci possono creare modelli di dati personalizzati che supportano i casi di utilizzo di marketing con i dati di Experience Platform.
