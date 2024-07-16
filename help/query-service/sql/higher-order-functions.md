---
title: Gestire tipi di dati array e mapping con funzioni di ordine superiore
description: Scopri come gestire array e mappare tipi di dati con funzioni di ordine superiore in Query Service. Sono forniti esempi pratici per i casi d’uso comuni.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Gestire tipi di dati array e mapping con funzioni di ordine superiore

Utilizzare questa guida per scoprire come le funzioni di ordine superiore possono elaborare tipi di dati complessi, ad esempio array e mappe. Queste funzioni eliminano la necessità di esplodere l&#39;array, eseguono una funzione e combinano il risultato. Le funzioni di ordine più elevato sono particolarmente utili per analizzare o elaborare set di dati e analisi di serie temporali, che spesso presentano strutture nidificate complesse, array, mappe e diversi casi d’uso.

Il seguente elenco di casi d’uso contiene esempi di funzioni di manipolazione di array e mappe di ordine più elevato.

## Utilizza trasformazione per adeguare il totale del prezzo di n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

Lo snippet di cui sopra applica una funzione a ciascun elemento dell’array e restituisce un nuovo array di elementi trasformati. In particolare, la funzione `transform` utilizza un array di tipo T e converte ogni elemento dal tipo T al tipo U. Restituisce quindi un array di tipo U. I tipi effettivi T e U dipendono dall&#39;uso specifico della funzione di trasformazione.

`transform(array<T>, function<T, Int, U>): array<U>`

Questa funzione di trasformazione di matrice è simile all&#39;esempio precedente, ma esistono due argomenti per la funzione. Il secondo argomento di questa funzione riceve anche l&#39;indice dell&#39;elemento nell&#39;array oltre a essere trasformato.

**Esempio**

L’esempio SQL seguente illustra questo caso d’uso. La query recupera un set limitato di righe dalla tabella specificata, trasformando l&#39;array `productListItems` moltiplicando l&#39;attributo `priceTotal` di ogni elemento per 73. Il risultato include le colonne `_id`, `productListItems` e `price_in_inr` trasformate. La selezione si basa su un intervallo di timestamp specifico.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Viene utilizzato per scoprire se esiste un prodotto con una SKU specifica {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

Nel frammento precedente, la funzione `exists` viene applicata a ogni elemento dell&#39;array e restituisce un valore booleano. Il valore booleano indica se nell’array sono presenti uno o più elementi che soddisfano una condizione specificata. In questo caso, conferma l’esistenza di un prodotto con una SKU specifica.

**Esempio**

Nell&#39;esempio SQL seguente, la query recupera `productListItems` dalla tabella `geometrixxx_999_xdm_pqs_1batch_10k_rows` e valuta se esiste un elemento con uno SKU uguale a `123679` nell&#39;array `productListItems`. Quindi filtra i risultati in base a un intervallo specifico di marche temporali e limita i risultati finali a dieci righe.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Utilizza il filtro per trovare i prodotti in cui SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Questa funzione filtra una matrice di elementi in base a una determinata condizione che valuta ogni elemento come valore booleano. Restituisce quindi un nuovo array che include solo elementi in cui la condizione ha restituito un valore true.

**Esempio**

La query seguente seleziona la colonna `productListItems`, applica un filtro per includere solo elementi con SKU maggiore di 100000 e limita il set di risultati alle righe all&#39;interno di un intervallo di timestamp specifico. L&#39;array filtrato viene quindi impostato come `_filter` nell&#39;output.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Utilizza aggregato per sommare gli SKU di tutte le voci dell’elenco prodotti associate a un ID specifico e raddoppiare il totale risultante {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Questa operazione di aggregazione applica un operatore binario a uno stato iniziale e a tutti gli elementi dell&#39;array. Inoltre, riduce più valori a un singolo stato. Dopo questa riduzione, lo stato finale viene quindi convertito nel risultato finale utilizzando una funzione di fine. La funzione di finitura prende l&#39;ultimo stato ottenuto dopo aver applicato l&#39;operatore binario a tutti gli elementi dell&#39;array e fa qualcosa con esso per produrre il risultato finale.

**Esempio**

Questo esempio di query calcola il valore SKU massimo dall&#39;array `productListItems` entro l&#39;intervallo di timestamp specificato e raddoppia il risultato. L&#39;output include l&#39;array `productListItems` originale e l&#39;array `max_value` calcolato.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Utilizza zip_with per assegnare un numero di sequenza a tutti gli elementi nell’elenco dei prodotti {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Questo snippet combina gli elementi di due array in un unico nuovo array. L&#39;operazione viene eseguita in modo indipendente su ciascun elemento dell&#39;array e genera coppie di valori. Se una matrice è più breve, vengono aggiunti valori Null per corrispondere alla lunghezza della matrice più lunga. Ciò si verifica prima dell’applicazione della funzione.

**Esempio**

La query seguente utilizza la funzione `zip_with` per creare coppie di valori da due array. A tale scopo, aggiungere i valori SKU dell&#39;array `productListItems` a una sequenza di numeri interi generata utilizzando la funzione `Sequence`. Il risultato viene selezionato insieme alla colonna `productListItems` originale ed è limitato in base a un intervallo di timestamp.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Utilizzare map_from_entries per assegnare un numero di sequenza a ciascun elemento dell&#39;elenco dei prodotti e ottenere il risultato finale come mappa {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Questo snippet converte un array di coppie chiave-valore in una mappa. È utile quando si tratta di dati di coppie chiave-valore che potrebbero beneficiare di una struttura più organizzata ed efficiente.

**Esempio**

La query seguente crea coppie di valori da una sequenza e dall&#39;array productListItems, converte tali coppie in una mappa utilizzando map_from_entries, quindi seleziona la colonna productListItems originale insieme alla nuova colonna map_from_entries creata. Il risultato viene filtrato e limitato in base all’intervallo di marca temporale specificato.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilizza map_form_arrays per assegnare numeri di sequenza agli elementi nell’elenco dei prodotti e restituire il risultato come mappa {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

La funzione `map_form_arrays` crea una mappa utilizzando i valori accoppiati di due array.

>[!IMPORTANT]
>
>Nelle chiavi non devono essere presenti elementi null.

**Esempio**

L&#39;istruzione SQL seguente crea una mappa in cui le chiavi sono numeri in sequenza generati utilizzando la funzione `Sequence` e i valori sono elementi dell&#39;array `productListItems`. La query seleziona la colonna `productListItems` e utilizza la funzione `Map_from_arrays` per creare la mappa in base alla sequenza di numeri generata e agli elementi dell&#39;array. Il risultato è limitato a dieci righe e filtrato in base a un intervallo di marca temporale.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilizza map_concat per concatenare due mappe in come mappa singola {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

La funzione `map_concat` nel frammento precedente accetta più mappe come argomenti e restituisce una nuova mappa che combina tutte le coppie chiave-valore dalle mappe di input. La funzione concatena più mappe in una singola mappa e la mappa risultante include tutte le coppie chiave-valore dalle mappe di input.

**Esempio**

L&#39;istruzione SQL seguente crea una mappa in cui ogni elemento in `productListItems` è associato a un numero di sequenza, che viene quindi concatenato con un&#39;altra mappa in cui le chiavi vengono generate in un intervallo di sequenza specifico.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilizza element_at per recuperare un valore corrispondente a &quot;AAID&quot; nella mappa delle identità per un ulteriore calcolo {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

Per le matrici, il frammento restituisce l&#39;elemento in corrispondenza di un indice specificato (basato su 1) o il valore associato a una chiave in una mappa. Se l&#39;indice è &lt; 0, accede agli elementi dall&#39;ultimo al primo e restituisce null se l&#39;indice supera la lunghezza della matrice.

Per le mappe, restituisce un valore per la chiave specificata o null se la chiave non è contenuta nella mappa.

**Esempio**

La query seleziona la colonna `identitymap` dalla tabella `geometrixxx_999_xdm_pqs_1batch_10k_rows` ed estrae il valore associato alla chiave `AAID` per ogni riga. I risultati sono limitati alle righe che rientrano nell’intervallo di marca temporale specificato e la query limita l’output a dieci righe.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Utilizza la cardinalità per trovare il numero di identità nella mappa delle identità {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Questo snippet restituisce le dimensioni di una matrice o mappa specificata e fornisce un alias. Restituisce -1 se il valore è null.

**Esempio**

La query seguente recupera la colonna `identitymap` e la funzione `Cardinality` calcola il numero di elementi in ogni mappa all&#39;interno di `identitymap`. I risultati sono limitati a dieci righe e vengono filtrati in base a un intervallo di marca temporale specificato.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Utilizzare array_distinct per trovare gli elementi distinti in productListItems {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

Lo snippet di cui sopra rimuove i valori duplicati dall’array specificato.

**Esempio**

La query seguente seleziona la colonna `productListItems`, rimuove gli elementi duplicati dagli array e limita l&#39;output a dieci righe in base a un intervallo di timestamp specificato.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Risultato**

I risultati per questa istruzione SQL saranno simili a quelli riportati di seguito.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Funzioni di ordine superiore aggiuntive {#additional-higher-order-functions}

I seguenti esempi di funzioni di ordine superiore sono spiegati come parte del caso di utilizzo del recupero di record simili. Un esempio e una spiegazione dell’utilizzo di ciascuna funzione sono forniti nella rispettiva sezione di tale documento.

L&#39;esempio di funzione [`transform`](../use-cases/retrieve-similar-records.md#length-adjustment) riguarda la tokenizzazione di un elenco di prodotti.

L&#39;esempio della funzione [`filter`](../use-cases/retrieve-similar-records.md#filter-results) dimostra un&#39;estrazione più precisa e precisa delle informazioni rilevanti dai dati di testo.

La funzione [`reduce`](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) consente di derivare valori cumulativi o aggregati, che possono essere fondamentali in vari processi di analisi e pianificazione.
