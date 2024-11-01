---
title: Tecniche di trasformazione delle feature
description: Scopri le tecniche di pre-elaborazione essenziali come la trasformazione dei dati, la codifica e il ridimensionamento delle funzioni, che preparano i dati per l’apprendimento dei modelli statistici. Descrive l'importanza di gestire i valori mancanti e di convertire i dati di categoria per migliorare le prestazioni e la precisione del modello.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '3437'
ht-degree: 8%

---

# Tecniche di trasformazione delle feature

Le trasformazioni sono fasi di pre-elaborazione cruciali che convertono o scalano i dati in un formato adatto all&#39;apprendimento e all&#39;analisi dei modelli, garantendo prestazioni e precisione ottimali. Questo documento funge da risorsa di sintassi supplementare e fornisce dettagli approfonditi sulle tecniche di trasformazione delle funzioni chiave per la preelaborazione dei dati.

I modelli di apprendimento automatico non possono elaborare direttamente valori stringa o valori null, rendendo essenziale la preelaborazione dei dati. Questa guida spiega come utilizzare varie trasformazioni per imputare i valori mancanti, convertire i dati categorici in formati numerici e applicare tecniche di ridimensionamento delle funzioni come la codifica a caldo e la vettorizzazione. Questi metodi consentono ai modelli di interpretare e apprendere efficacemente dai dati, migliorando in ultima analisi le loro prestazioni.

## Trasformazione automatica delle feature {#automatic-transformations}

Se si sceglie di ignorare la clausola `TRANSFORM` nel comando `CREATE MODEL`, la trasformazione della funzionalità viene eseguita automaticamente. La preelaborazione automatica dei dati include la sostituzione nulla e le trasformazioni di funzionalità standard (in base al tipo di dati). Le colonne numeriche e di testo vengono imputate automaticamente, quindi le trasformazioni delle funzioni vengono eseguite per garantire che i dati siano in un formato appropriato per l’apprendimento automatico dei modelli. Questo processo include l’imputazione dei dati mancanti e le trasformazioni categoriche, numeriche e booleane.

>[!IMPORTANT]
>
>La trasformazione della feature utilizzata al momento della formazione verrà utilizzata anche per la trasformazione della feature al momento della previsione e della valutazione.

Nelle tabelle seguenti viene illustrato come vengono gestiti diversi tipi di dati quando la clausola `TRANSFORM` viene omessa durante il comando `CREATE MODEL`.

### Sostituzione nulla {#automatic-null-replacement}

| Tipo di dati | Sostituzione nulla |
|-----------------|-----------------------------------------------------|
| Numerico | I valori Null vengono sostituiti con il valore medio della colonna. |
| Categorico | I valori Null vengono sostituiti con la parola chiave `ml_unknown`. |
| Booleano | I valori Null vengono sostituiti con un valore `FALSE`. |
| Timestamp | Questo dovrebbe essere un campo continuo. |
| Nidificato/STRUCT | La sostituzione dipende dal tipo di dati del nodo foglia. |

### Trasformazione delle feature {#automatic-feature-transformation}

| Tipo di dati | Trasformazione della feature |
|-----------------|-----------------------------------------------------|
| Numerico | NON RICHIESTO: poiché questo tipo di dati è compreso dagli algoritmi di apprendimento automatico. |
| Stringa | Viene eseguita l&#39;indicizzazione della stringa. |
| Booleano | Viene eseguita l&#39;indicizzazione della stringa. |
| Timestamp | Non si verifica alcuna operazione. |
| STRUCT | Il valore viene espanso fino al relativo nodo foglia. La trasformazione si verifica in base al tipo di dati del nodo foglia. |

**esempio**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Trasformazioni di feature manuali {#manual-transformations}

Per definire la preelaborazione dei dati personalizzati nell&#39;istruzione `CREATE MODEL`, utilizzare la clausola `TRANSFORM` in combinazione con un numero qualsiasi di funzioni di trasformazione disponibili. Queste funzioni di pre-elaborazione manuale possono essere utilizzate anche al di fuori della clausola `TRANSFORM`. Tutte le trasformazioni descritte nella sezione [trasformatore seguente](#available-transformations) possono essere utilizzate per la preelaborazione manuale dei dati.

### Caratteristiche principali

Di seguito sono riportate le caratteristiche chiave della trasformazione delle feature da considerare quando definite le funzioni di pre-elaborazione:

- **Sintassi**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Il nome alias è obbligatorio nella sintassi. È necessario fornire un nome di alias per evitare che la query abbia esito negativo.

- **Parametri**: i parametri sono argomenti posizionali. Ciò significa che ogni parametro può accettare solo determinati valori. Per informazioni dettagliate su quale funzione utilizza un determinato argomento, consulta la documentazione pertinente.

- **Trasformatori concatenamento**: l&#39;output di un trasformatore può diventare l&#39;input di un altro trasformatore.

- **Utilizzo funzionalità**: l&#39;ultima trasformazione funzionalità viene utilizzata come funzionalità del modello di apprendimento automatico.

**Esempio**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Trasformazioni disponibili {#available-transformations}

Sono disponibili 19 trasformazioni. Queste trasformazioni sono suddivise in [trasformazioni generali](#general-transformations), [trasformazioni numeriche](#numeric-transformations), [trasformazioni categoriche](#categorical-transformations) e [trasformazioni testuali](#textual-transformations).

### Trasformazioni generali {#general-transformations}

Leggi questa sezione per informazioni dettagliate sui trasformatori utilizzati per un’ampia gamma di tipi di dati. Queste informazioni sono essenziali se devi applicare trasformazioni che non sono specifiche per dati categorici o testuali.

>[!NOTE]
>
>Il tipo di dati di input si riferisce alla colonna alla quale viene applicata l’imputazione. Il tipo di dati di output si riferisce alla colonna che viene prodotta come output dopo l’entrata in vigore della trasformazione.

#### Imputer numerico {#numeric-imputer}

Il trasformatore **Numeric imputer** completa i valori mancanti in un set di dati. Questa opzione utilizza la media, la mediana o la modalità delle colonne in cui si trovano i valori mancanti. Le colonne di input devono essere `DoubleType` o `FloatType`. Ulteriori informazioni ed esempi sono disponibili nella [documentazione sull&#39;algoritmo Spark](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Tutti i valori Null nelle colonne di input vengono considerati mancanti e quindi vengono anche imputati.

**Tipi di dati**

- Tipo di dati di input: numerico
- Tipo di dati di output: numerico

**Definizione**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Una strategia di imputazione. I valori disponibili sono: [`mean`, `median`, `mode`]. | stringa | media | facoltativo |

{style="table-layout:auto"}

**Esempio prima dell&#39;imputazione**

| id | ora |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Esempio dopo imputazione (utilizzando la strategia media)**

| id | ora |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Imputer stringa {#string-imputer}

Il trasformatore **String imputer** completa i valori mancanti in un set di dati utilizzando una stringa fornita dall&#39;utente come argomento di funzione. Le colonne di input e output devono essere del tipo di dati `string`.

>[!NOTE]
>
>Tutti i valori Null nelle colonne di input vengono considerati mancanti e vengono sostituiti dalla stringa specificata.

**Tipi di dati**

- Tipo di dati di input: String
- Tipo di dati di output: String

**Definizione**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Valore che sostituisce i valori Null. | stringa | ml_unknown | facoltativo |

{style="table-layout:auto"}

**Esempio prima dell&#39;imputazione**

| id | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Esempio dopo imputazione (utilizzando &#39;ml_unknown&#39; come sostituto)**

| id | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Imputer booleano {#imputer}

Il trasformatore **Boolean imputer** completa i valori mancanti in un set di dati per una colonna booleana. Le colonne di input e output devono essere di tipo `Boolean`.

>[!NOTE]
>
>Tutti i valori Null nelle colonne di input vengono considerati mancanti e vengono sostituiti dal valore booleano specificato.

**Tipi di dati**

- Tipo di dati di input: booleano
- Tipo di dati di output: booleano

**Definizione**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Imputatore booleano. Valori consentiti: [`true`, `false`]. | booleano | false | facoltativo |

**Esempio prima dell&#39;imputazione**

| id | contrassegno |
|---|---|
| 0 | true |
| 1 | null |
| 2 | false |

**Esempio dopo imputazione (utilizzando &#39;true&#39; come sostituto)**

| id | contrassegno |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### Assemblatore vettoriale {#vector-assembler}

Il trasformatore `VectorAssembler` combina un elenco specificato di colonne di input in un&#39;unica colonna vettoriale, semplificando la gestione di più funzionalità nei modelli di apprendimento automatico. Questo è particolarmente utile per unire le feature grezze e quelle generate da diversi trasformatori di feature in un unico vettore di feature unificato. `VectorAssembler` accetta colonne di input di tipo numerico, booleano e vettoriale. In ogni riga, i valori delle colonne di input vengono concatenati in un vettore nell&#39;ordine specificato.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Tipi di dati**

- Tipo di dati di input: `array[string]` (nomi di colonna con valori numerici/matrice[numerici])
- Tipo di dati di output: `Vector[double]`

**Definizione**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
| -------- | ------------ | ----- | -------- | -------- |
| NA | Per questo trasformatore non sono necessari parametri aggiuntivi. | NA | NA | NA |

{style="table-layout:auto"}

**Esempio prima della trasformazione**

| id | ora | dispositivi mobili | userFeatures | cliccato |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0,0, 10,0, 0,5] | 1,0 |

{style="table-layout:auto"}

**Esempio dopo trasformazione**

| id | ora | dispositivi mobili | userFeatures | cliccato | funzioni |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0,0, 10,0, 0,5] | 1,0 | [18,0, 1,0, 0,0, 10,0, 0,5] |

{style="table-layout:auto"}

### Trasformazioni numeriche {#numeric-transformations}

Leggi questa sezione per scoprire i trasformatori disponibili per l’elaborazione e il ridimensionamento dei dati numerici. Questi trasformatori sono necessari per gestire e ottimizzare le funzioni numeriche nei set di dati.

#### Binarizzatore {#binarizer}

Il trasformatore `Binarizer` converte le funzionalità numeriche in funzionalità binarie (0/1) tramite un processo denominato binarizzazione. I valori delle feature superiori alla soglia specificata vengono convertiti in 1,0, mentre i valori uguali o inferiori alla soglia vengono convertiti in 0,0. `Binarizer` supporta sia `Vector` che `Double` tipi per la colonna di input.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Tipi di dati**

- Tipo di dati di input: colonna numerica
- Tipo di dati di output: numerico

**Definizione**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Parametro per la soglia utilizzata per binarizzare feature continue. Le funzioni maggiori della soglia vengono binalizzate a 1.0, mentre le funzioni uguali o inferiori alla soglia vengono binarie a 0.0. | int/double | 0,0 | facoltativo |

{style="table-layout:auto"}

**Input di esempio prima della binarizzazione**

| id | valutazione |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Output di esempio dopo la binarizzazione (soglia predefinita di 0,0)**

| id | valutazione |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definizione con soglia personalizzata**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Output di esempio dopo la binarizzazione (con una soglia di 14,0)**

| id | età |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

Il trasformatore `Bucketizer` converte una colonna di funzionalità continue in una colonna di contenitori di funzionalità, in base alle soglie specificate dall&#39;utente. Questo processo è utile per segmentare i dati continui in contenitori o bucket discreti. `Bucketizer` richiede un parametro `splits`, che definisce i limiti dei bucket.

**Tipi di dati**

- Tipo di dati di input: colonna numerica
- Tipo di dati di output: numerico (valori associati)

**Definizione**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Parametro per la mappatura di feature continue in bucket. Con `n+1` divisioni, sono presenti `n` bucket. Le divisioni devono essere in ordine rigorosamente crescente e l’intervallo (x,y) viene utilizzato per ciascun bucket ad eccezione dell’ultimo, che include y. | array (doppio) | N/D | facoltativo |

{style="table-layout:auto"}

**Esempi di divisioni**

- Array(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Array(0,0, 1,0, 2,0)

Le [PROD143]e devono coprire l&#39;intero intervallo di valori Double. In caso contrario, i valori al di fuori delle [PROD143]e specificate verranno trattati come errori.

**Esempio di trasformazione**

Questo esempio prende una colonna di funzioni continue (`course_duration`), la racchiude in base al `splits` fornito e quindi assembla i bucket risultanti con altre funzioni.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Il trasformatore `MinMaxScaler` ridimensiona ogni funzione in un set di dati di righe vettoriali a un intervallo specificato, in genere [0, 1]. In questo modo tutte le feature contribuiscono allo stesso modo al modello. Questa funzione è particolarmente utile per i modelli sensibili alla modifica in scala delle feature, ad esempio per gli algoritmi basati sulla discendenza con gradiente. `MinMaxScaler` funziona sui seguenti parametri:

- **min**: il limite inferiore della trasformazione, condiviso da tutte le funzionalità. Il valore predefinito è `0.0`.
- **max**: limite superiore della trasformazione, condiviso da tutte le funzionalità. Il valore predefinito è `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Tipi di dati**

- Tipo di dati di input: `Array[Double]`
- Tipo di dati di output: `Array[Double]`

**Definizione**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Limite inferiore dopo la trasformazione, condiviso da tutte le feature. | doppio | 0,0 | facoltativo |
| `max` | Limite superiore dopo la trasformazione, condiviso da tutte le feature. | doppio | 1,0 | facoltativo |

**Esempio di trasformazione**

Questo esempio trasforma un insieme di feature, ridimensionandole all&#39;intervallo specificato utilizzando MinMaxScaler dopo l&#39;applicazione di diverse altre trasformazioni.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Il trasformatore `MaxAbsScaler` ridimensiona ogni funzione in un set di dati di righe vettoriali all&#39;intervallo [-1, 1] dividendo per il valore assoluto massimo di ogni funzione. Questa trasformazione è ideale per preservare la sparsità nei set di dati con valori sia positivi che negativi, in quanto non sposta o centra i dati. Questo rende `MaxAbsScaler` particolarmente adatto per i modelli sensibili alla scala delle funzioni di input, come ad esempio quelli che prevedono calcoli di distanza.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Tipi di dati**

- Tipo di dati di input: `Array[Double]`
- Tipo di dati di output: `Array[Double]`

**Definizione**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| NA | MaxAbsScaler non richiede parametri aggiuntivi per il suo funzionamento. | NA | NA | NA |

**Esempio di trasformazione**

In questo esempio vengono applicate diverse trasformazioni, tra cui `MaxAbsScaler`, per ridimensionare le funzionalità nell&#39;intervallo [-1, 1].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalizzatore {#normalizer}

`Normalizer` è un trasformatore che normalizza ogni vettore in un set di dati di righe vettoriali per avere una norma unitaria. Questo processo assicura una scala coerente senza alterare la direzione dei vettori. Questa trasformazione è particolarmente utile nei modelli di apprendimento automatico che si basano su misurazioni di distanza o altri calcoli basati su vettori, specialmente quando la grandezza dei vettori varia in modo significativo.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Tipi di dati**

- Tipo di dati di input: `array[double]` / `vector[double]`
- Tipo di dati di output: `vector[double]`

**Definizione**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Specifica `p-norm` utilizzato per la normalizzazione (ad esempio `1-norm`, `2-norm`, ecc.). | intero | 2 | facoltativo |

**Esempio di trasformazione**

In questo esempio viene illustrato come applicare diverse trasformazioni, incluso `Normalizer`, per normalizzare un set di funzionalità utilizzando `p-norm` specificato.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer` è un trasformatore che converte una colonna con caratteristiche continue in caratteristiche categoriche unite, con il numero di raccoglitori determinato dal parametro `numBuckets`. In alcuni casi, il numero effettivo di bucket può essere inferiore al numero specificato se sono presenti troppi pochi valori distinti per creare un numero sufficiente di quantili.

Questa trasformazione è particolarmente utile per semplificare la rappresentazione dei dati continui o per prepararla per gli algoritmi che funzionano meglio con l’input categoriale.

**Tipi di dati**

- Tipo di dati di input: colonna numerica
- Tipo di dati di output: colonna numerica (categorica)

**Definizione**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Il numero di bucket (quantili o categorie) in cui vengono raggruppati i punti dati. Questo numero deve essere maggiore o uguale a due. | intero | 2 | facoltativo |

**Esempio di trasformazione**

In questo esempio viene illustrato come `QuantileDiscretizer` racchiude una colonna di funzionalità continue (`hour`) in tre bucket categorici.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Esempio prima e dopo la discretizzazione**

| id | ora | risultato |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1,0 |
| 3 | 5.0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

`StandardScaler` è un trasformatore che normalizza ogni funzionalità in un set di dati di righe vettoriali in modo che abbia una deviazione standard unitaria e/o una media pari a zero. Questo processo rende i dati più adatti per gli algoritmi che presumono che le funzioni siano centrate intorno allo zero con una scala coerente. Questa trasformazione è particolarmente importante per i modelli di apprendimento automatico come SVM, regressione logistica e reti neurali, in cui dati non standardizzati potrebbero portare a problemi di convergenza o a una precisione ridotta.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Tipi di dati**

- Tipo di dati di input: vettoriale
- Tipo di dati di output: vettoriale

**Definizione**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Ridimensiona i dati in modo che abbiano una deviazione standard unitaria. | booleano | True | facoltativo |
| `withMean` | Centra i dati con la media prima del ridimensionamento. Questa opzione produce un output denso, pertanto occorre prestare attenzione con l&#39;input sparso. | booleano | False | facoltativo |

**Esempio di trasformazione**

In questo esempio viene illustrato come applicare StandardScaler a un insieme di feature, normalizzandole con deviazione standard unitaria e media zero.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Trasformazioni categoriche {#categorical-transformations}

Leggi questa sezione per una panoramica dei trasformatori disponibili progettati per convertire e pre-elaborare dati categorici per modelli di apprendimento automatico. Queste trasformazioni sono progettate per punti dati che rappresentano categorie o etichette distinte, anziché valori numerici.

#### StringIndexer {#stringindexer}

`StringIndexer` è un trasformatore che codifica una colonna stringa di etichette in una colonna di indici numerici. Gli indici variano da 0 a `numLabels` e sono ordinati per frequenza di etichetta (l&#39;etichetta più frequente riceve un indice pari a 0). Se la colonna di input è numerica, viene inserita in una stringa prima dell’indicizzazione. Le etichette non visualizzate possono essere assegnate all&#39;indice `numLabels` se specificato dall&#39;utente.

Questa trasformazione è particolarmente utile per convertire i dati stringa categorici in forma numerica, rendendoli adatti a modelli di apprendimento automatico che richiedono input numerici.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Tipi di dati**

- Tipo di dati di input: String
- Tipo di dati di output: numerico

**Definizione**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|-------------|------|---------|----------|
| NA | `StringIndexer` non richiede parametri aggiuntivi per l&#39;operazione. | NA | NA | NA |

**Esempio di trasformazione**

In questo esempio viene illustrato come applicare `StringIndexer` a una funzionalità categorica, convertendola in un indice numerico.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder` è un trasformatore che converte una colonna di indici di etichetta in una colonna di vettori binari sparsi, dove ogni vettore ha al massimo un singolo valore. Questa codifica è particolarmente utile per consentire agli algoritmi che richiedono un input numerico, come la regressione logistica, di incorporare in modo efficace dati categorici.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Tipi di dati**

- Tipo di dati di input: numerico
- Tipo di dati di output: Vector[Int]

**Definizione**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|-------------|------|---------|----------|
| NA | OneHotEncoder non richiede parametri aggiuntivi per il suo funzionamento. | NA | NA | NA |

**Esempio di trasformazione**

In questo esempio viene illustrato come applicare `StringIndexer` a una funzionalità categorica e quindi utilizzare `OneHotEncoder` per convertire i valori indicizzati in un vettore binario.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Trasformazioni testuali {#textual-transformations}

Questa sezione fornisce dettagli sui trasformatori disponibili per l’elaborazione e la conversione di dati testuali in formati utilizzabili dai modelli di apprendimento automatico. Questa sezione è fondamentale per gli sviluppatori che lavorano con dati in linguaggio naturale e analisi testuale.

#### CountVectorizer {#countvectorizer}

`CountVectorizer` è un trasformatore che converte una raccolta di documenti di testo in vettori di conteggi di token, producendo rappresentazioni sparse basate sul vocabolario estratto dal corpo. Questa trasformazione è essenziale per convertire i dati di testo in un formato numerico che può essere utilizzato dagli algoritmi di machine learning, come LDA (Latent Dirichlet Allocation), rappresentando la frequenza dei token all&#39;interno di ciascun documento.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Tipi di dati**

- Tipo di dati di input: Array[String]
- Tipo di dati di output: vettore denso

**Definizione**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Dimensione massima del vocabolario. CountVectorizer crea un vocabolario che considera solo i primi `vocabSize` termini ordinati in base alla frequenza dei termini all&#39;interno del corpo. | Intero | 218 | facoltativo |
| `MIN_DOC_FREQ` | Specifica il numero minimo di documenti diversi in cui un termine deve essere incluso nel vocabolario. Può essere un numero assoluto o una frazione di documenti (se doppio). | Doppio | 1,0 | facoltativo |
| `MAX_DOC_FREQ` | Specifica il numero massimo di documenti diversi in cui un termine può essere incluso nel vocabolario. Può essere un numero assoluto o una frazione di documenti (se doppio). | Doppio | (263)-1 | facoltativo |
| `MIN_TERM_FREQ` | Consente di escludere le parole rare in un documento. I termini con frequenza/conteggio inferiore alla soglia specificata vengono ignorati. Può essere un numero assoluto o una frazione del numero di token del documento. | Doppio | 1,0 | facoltativo |

{style="table-layout:auto"}

**Esempio di trasformazione**

In questo esempio viene illustrato come CountVectorizer converte una raccolta di matrici di testo in vettori di conteggi di token, generando una rappresentazione sparsa.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Esempio prima e dopo la vettorizzazione**

| id | testi | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1,0,1,0,1,0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram` è un trasformatore che genera una sequenza di n-grammi, dove un n-grammo è una sequenza di (&#39;??&#39;) token (in genere parole) per un numero intero (`𝑛`). L’output è costituito da stringhe delimitate da spazi di parole consecutive &quot;??&quot;, che possono essere utilizzate come funzioni nei modelli di apprendimento automatico, in particolare quelli incentrati sull’elaborazione del linguaggio naturale.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Tipi di dati**

- Tipo di dati di input: Array[String]
- Tipo di dati di output: Array[String]

**Definizione**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | La lunghezza minima in grammi deve essere maggiore o uguale a 1. | intero | 2 (caratteristiche bigram) | facoltativo |

{style="table-layout:auto"}

**Esempio di trasformazione**

Questo esempio illustra come il trasformatore NGram crea una sequenza di 3 grammi da un elenco di token derivati dai dati di testo.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Esempio prima e dopo trasformazione n grammi**

| id | testi | n_token |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;entertaining&quot;, &quot;movie&quot;] | [&quot;era un&quot;, &quot;era un divertente&quot;, &quot;un film divertente&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover` è un trasformatore che rimuove le parole non significative da una sequenza di stringhe, filtrando le parole comuni che non hanno un significato significativo. Come input viene utilizzata una sequenza di stringhe (ad esempio l&#39;output di un token) e vengono rimosse tutte le parole non significative specificate dal parametro `stopWords`.

Questa trasformazione è utile per la pre-elaborazione dei dati testuali, migliorando l’efficacia dei modelli di apprendimento automatico a valle eliminando le parole che non contribuiscono molto al significato generale.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Tipi di dati**

- Tipo di dati di input: Array[String]
- Tipo di dati di output: Array[String]

**Definizione**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Le parole da escludere. | matrice [stringa] | Impostazione predefinita: parole non significative in inglese | facoltativo |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Esempio di trasformazione**

In questo esempio viene illustrato come `StopWordsRemover` esclude le parole non significative comuni in inglese da un elenco di token.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Rimozione delle parole di interruzione prima e dopo**

| id | raw | filtrato |
|----|------------------------------|--------------------------|
| 0 | [Ho visto, il, rosso, palloncino] | [sega, rosso, fumetto] |
| 1 | [Mary, aveva, poco, agnello] | [Maria, piccola, agnello] |

**Esempio con parole di interruzione personalizzate**

In questo esempio viene illustrato come utilizzare un elenco personalizzato di parole non significative per filtrare parole specifiche dalle sequenze di input.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Rimozione delle parole non significative personalizzate prima e dopo**

| id | raw | filtrato |
|----|------------------------------|--------------------------|
| 0 | [Ho visto, il, rosso, palloncino] | [ha visto,, fumetto] |
| 1 | [Mary, aveva, poco, agnello] | [Maria, piccola, agnello] |

#### TF-IDF {#tf-idf}

`TF-IDF` (Term Frequency-Inverse Document Frequency) è un trasformatore utilizzato per misurare l&#39;importanza di una parola all&#39;interno di un documento rispetto a un corpus. Frequenza termine (TF) si riferisce al numero di volte in cui un termine \(t\) viene visualizzato in un documento \(d\), mentre la frequenza documento (DF) misura il numero di documenti nel corpo \(D\) contengono il termine \(t\). Questo metodo è ampiamente utilizzato nell&#39;estrazione di testo per ridurre l&#39;influenza di parole comunemente presenti, come &quot;a&quot;, &quot;the&quot; e &quot;of&quot;, che contengono poche informazioni univoche.

Questa trasformazione è particolarmente utile nelle attività di estrazione del testo e di elaborazione del linguaggio naturale, in quanto assegna un valore numerico all&#39;importanza di ogni parola all&#39;interno di un documento e in tutto il corpo.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Tipi di dati**

- Tipo di dati di input: Array[String]
- Tipo di dati di output: Vector[Int]

**Definizione**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Numero di feature da generare. Deve essere maggiore di 0. | Intero | 262144 | facoltativo |
| `MIN_DOC_FREQ` | Numero minimo di documenti in cui un termine deve apparire incluso nel modello. | Intero | 0 | facoltativo |

{style="table-layout:auto"}

**Esempio di trasformazione**

Questo esempio illustra come utilizzare TF-IDF per trasformare frasi tokenizzate in un vettore di funzione che rappresenta l’importanza di ogni termine nel contesto dell’intero corpus.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

`Tokenizer` è un trasformatore che suddivide il testo, ad esempio una frase, in singoli termini, in genere parole. Converte le frasi in array di token, fornendo un passaggio fondamentale nella preelaborazione del testo che prepara i dati per ulteriori processi di analisi del testo o modellazione.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Tipi di dati**

- Tipo di dati di input: frase testuale
- Tipo di dati di output: Array[String]

**Definizione**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|-----------|-------------|------|---------|----------|
| NA | `Tokenizer` non richiede parametri aggiuntivi per l&#39;operazione. | NA | NA | NA |

**Esempio di trasformazione**

In questo esempio viene illustrato come `Tokenizer` suddivide le frasi in singole parole (token) come parte di una pipeline di elaborazione del testo.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec` è uno stimatore che elabora sequenze di parole che rappresentano documenti e addestra un `Word2VecModel`. Questo modello mappa ogni parola su un unico vettore a dimensione fissa e trasforma ogni documento in un vettore calcolando la media dei vettori di tutte le parole del documento. Ampiamente utilizzato nelle attività di elaborazione del linguaggio naturale, `Word2Vec` crea incorporamenti di parole che acquisiscono un significato semantico, convertendo i dati di testo in vettori numerici che rappresentano le relazioni tra le parole e consentendo un&#39;analisi più efficace del testo e modelli di apprendimento automatico.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Tipi di dati**

- Tipo di dati di input: Array[String]
- Tipo di dati di output: Vector[Double]

**Definizione**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parametri**

| Parametro | Descrizione | Tipo | Predefinito | Facoltativo |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | La dimensione del vettore in cui ogni parola viene trasformata. | Intero | 100 | facoltativo |
| `MIN_COUNT` | Numero minimo di volte per cui un token deve essere incluso nel vocabolario del modello `Word2Vec`. | Intero | 5 | facoltativo |

{style="table-layout:auto"}

**Esempio di trasformazione**

In questo esempio viene illustrato come `Word2Vec` converte una revisione tokenizzata in un vettore di dimensione fissa che rappresenta la media dei vettori di parola nel documento.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Esempio prima e dopo la trasformazione di Word2Vec**

| recensione | tokenizzato | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| questo era un film divertente | [questo, era, un, divertente, film] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.01515385233797133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.005757019785232843,-0.021328244300093502,0.009335877187550069] |

{style="table-layout:auto"}
