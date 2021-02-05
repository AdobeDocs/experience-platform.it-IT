---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;scintilla sql;Spark sql;spark;scintilla funzioni sql;funzioni;funzioni;'
solution: Experience Platform
title: Funzioni SQL Spark in Servizio query
topic: spark sql functions
description: Questa documentazione contiene informazioni sulle funzioni SQL Spark che estendono le funzionalità SQL.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '3893'
ht-degree: 1%

---


# [!DNL Spark] Funzioni SQL

Adobe Experience Platform Query Service fornisce diverse funzioni SQL Spark integrate per estendere le funzionalità SQL. In questo documento sono elencate le funzioni SQL Spark supportate da Query Service.

Per informazioni più dettagliate sulle funzioni, inclusi sintassi, utilizzo ed esempi, consultare la [Documentazione della funzione SQL Spark](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Non tutte le funzioni della documentazione esterna sono supportate.

## Categorie

- [Matematica e operatori statistici e funzioni](#math)
- [Operatori logici](#logical-operators)
- [Funzioni data/ora](#datetime-functions)
- [Array](#arrays)
- [Funzioni di inserimento dati](#datatype-casting)
- [Funzioni di conversione e formattazione](#conversion)
- [Valutazione dei dati](#data-evaluation)
- [Informazioni correnti](#current-information)
- [Funzioni di ordine superiore](#higher-order)

## Math e operatori statistici e funzioni {#math}

| Operatore/Funzione | Descrizione |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | Restituisce il resto dei due numeri |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | Moltiplica i due numeri |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Aggiunge i due numeri |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Sottrae i due numeri |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Divide i due numeri |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Restituisce il valore assoluto dell&#39;input |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Restituisce il valore del coseno inverso |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Restituisce la cardinalità stimata da HyperLogLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Restituisce il valore percentile approssimativo in base alla percentuale specificata |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Restituisce il valore del seno inverso |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Restituisce il valore tangente inverso |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Restituisce l&#39;angolo tra il piano positivo dell&#39;asse x e i punti indicati dalle coordinate |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Restituisce il valore medio |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Restituisce la radice del cubo |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) o [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Restituisce il numero intero più piccolo non più grande del valore immesso |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Converti da una base all&#39;altra |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Restituisce il coefficiente Pearson tra i numeri |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Restituisce il valore del coseno |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Restituisce il valore del coseno iperbolico |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Restituisce il valore cotangente |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Restituisce il grado di un valore in un gruppo di valori |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Restituisce il numero di Eulero |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Restituisce e alla potenza del valore |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Restituisce e alla potenza del valore meno 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Restituisce il fattoriale del valore |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Restituisce il numero intero più grande non inferiore al valore |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Restituisce il valore massimo di tutti i parametri |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Restituisce l&#39;ipotenusa dei due valori specificati |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Restituisce il valore della curtosi dal gruppo |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Restituisce il valore più piccolo di tutti i parametri |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Restituisce il logaritmo naturale del valore |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Restituisce il logaritmo del valore |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Restituisce il logaritmo, in base 10, del valore |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Restituisce il logaritmo del valore più 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Restituisce il logaritmo, in base 2, del valore |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Restituisce il valore massimo dell&#39;espressione |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Restituisce la media calcolata dai valori |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Restituisce il valore minimo dell&#39;espressione |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Restituisce ID con aumento monotonico |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Restituisce il valore negativo |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Restituisce la classificazione percentuale di un valore |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Restituisce il percentile esatto a una percentuale specificata |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Restituisce il percentile approssimativo ad una percentuale specificata |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Restituisce pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Restituisce il modulo positivo tra due valori |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Restituisce il valore positivo |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Restituisce il primo valore alla potenza del secondo valore |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Converte il valore in radianti |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Restituisce un numero casuale compreso tra 0 e 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Restituisce un valore casuale |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Restituisce il valore doppio più vicino |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Restituisce il valore arrotondato più vicino |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Restituisce il segno del numero |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Restituisce un intervallo del valore |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Restituisce il seno iperbolico del valore |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Restituisce la radice quadrata del valore |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Restituisce la deviazione standard del valore |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Restituisce la deviazione standard della popolazione del valore |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Restituisce la deviazione standard del campione del valore |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Restituisce la somma dei valori |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Restituisce tangente del valore |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Restituisce la tangente iperbolica del valore |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Restituisce la varianza della popolazione calcolata |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Restituisce la varianza calcolata del campione |

### Operatori logici e funzioni {#logical-operators}

| Operatore/Funzione | Descrizione |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) o [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Not logico |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Minore di |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Minore o uguale a |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | Uguale a |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Maggiore di |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Maggiore o uguale a |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Bitwise esclusive o |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Maggiore o uguale a |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Bitwise o |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitwise not |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Restituisce gli elementi comuni |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Assegna se l&#39;espressione è vera |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Se l&#39;espressione restituisce true, restituire la seconda espressione. In caso contrario, restituite la terza espressione. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Se l&#39;espressione è null, restituisce la seconda espressione. In caso contrario restituisce la prima espressione. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Restituisce true se la prima espressione si trova in una qualsiasi delle espressioni successive. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Restituisce true se il valore non è un numero |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Restituisce true se il valore non è null |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Restituisce true se il valore è null |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Restituisce la prima espressione, se non un numero, altrimenti restituisce la seconda espressione. |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Operatore logico |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Quando può essere utilizzato per creare condizioni di ramo per il confronto |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Restituisce true se l&#39;espressione XPath restituisce true o se viene trovato un nodo corrispondente |

### Funzioni data/ora {#datetime-functions}

| Funzione | Descrizione |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Aggiungi mesi alla data |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Aggiungi giorni alla data |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Modifica formato data |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Sottrai giorni dalla data |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Restituisce la data troncata all&#39;unità specificata |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Restituisce la differenza tra le date in giorni |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Restituisce il giorno del mese |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Restituisce il giorno della settimana (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Restituisce il giorno dell&#39;anno |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Restituisce la data in Unix ora |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Restituisce la data in base all&#39;ora UTC |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Restituisce l&#39;ora dell&#39;input |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Restituisce l&#39;ultimo giorno del mese a cui la data appartiene |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Restituisce il minuto dell&#39;input |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Restituisce il mese dell&#39;input |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Numero di mesi compresi tra |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Restituisce il primo giorno successivo all&#39;input |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Restituisce il quarto dell&#39;input |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Restituisce il secondo della stringa |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Converte la stringa in una data |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Converte la stringa in una marca temporale |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Converte la stringa in una marca temporale Unix |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Converte la stringa in una marca temporale UTC |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Tronca la data |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Restituisce il timestamp Unix |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Giorno della settimana (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Restituisce la settimana dell&#39;anno per una data specificata |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Restituisce l&#39;anno della stringa |

### Array {#arrays}

| Funzione | Descrizione |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Crea un array con gli elementi specificati |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Controlla se la matrice contiene il valore |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Rimuove valori duplicati dall&#39;array |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Restituisce un array degli elementi del primo array, ma non del secondo |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Restituisce l&#39;intersezione dei due array |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Unisce due array |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Restituisce il valore massimo dell&#39;array |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Restituisce il valore minimo dell&#39;array |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Restituisce la posizione basata su 1 dell&#39;elemento |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Rimuove tutti gli elementi uguali all&#39;elemento |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Crea un array contenente i valori contati per le ore |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Dispone l&#39;array |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Unisce l&#39;array, senza duplicazioni |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | ZIP |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Restituisce la dimensione dell&#39;array |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Restituisce l’elemento in posizione |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Elementi separati di array in più righe, escluso null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Elementi separati di array in più righe, incluso null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Restituisce la posizione basata su 1 dell&#39;array |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Appiattisce un array di array |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Array separato di strutture in una tabella, escluso null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Array separato di strutture in una tabella, incluso null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Elementi separati di array in più righe con posizioni, escluso null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Elementi separati di array in più righe con posizioni, incluso null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Inverti elementi della matrice |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Restituisce una permutazione casuale dell&#39;array |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Sottoinsiemi di un array |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Ordinare un array, in base a un ordine |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Unisce i due array in un singolo array, prima di applicare una funzione |

### Funzioni di inserimento dei tipi di dati {#datatype-casting}

| Funzione | Descrizione |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Cambia il tipo di dati in bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Cambia il tipo di dati in binario |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Cambia il tipo di dati in booleano |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Cambia il tipo di dati nel tipo specificato |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Cambia il tipo di dati in data |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Cambia il tipo di dati in decimale |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Cambia il tipo di dati in doppio |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Cambia il tipo di dati in mobile |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Cambia il tipo di dati in int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Cambia il tipo di dati in piccolo |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Creare una mappa da una stringa |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Cambia il tipo di dati in stringa |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Creare una struttura |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Cambia il tipo di dati in tinyint |

### Funzioni di conversione e formattazione {#conversion}

| Funzione | Descrizione |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Restituisce il valore numerico (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Cambia l&#39;argomento in una stringa base64 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Cambia l&#39;argomento in un valore binario |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Restituisce la lunghezza del bit |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Restituisce il carattere ASCII |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Restituisce la lunghezza della stringa |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Restituisce il valore del controllo di ridondanza ciclica |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Converti radianti in gradi |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Modificare il formato del numero |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Ottieni dati da JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Restituisce il valore hash |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Conversione dell&#39;argomento in un valore esadecimale |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Cambia la stringa da assegnare al titolo |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Cambia la stringa in lettere minuscole. |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Inserisce il lato sinistro di una stringa |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Creare una mappa |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Creare una mappa da un array |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Creare una mappa da un array di strutture |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Restituisce il valore md5 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Inserisce il lato destro di una stringa |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Rimuove gli spazi finali |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Restituisce il valore SHA1 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Restituisce il valore SHA2 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Restituire il codice del codice sorgente |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Separare i valori in righe |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Restituisce la sottostringa |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Restituisce una stringa JSON |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Sostituire i valori nella stringa |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Rimozione di caratteri iniziali e finali |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Cambia la stringa in maiuscolo |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Converte la stringa base64 in binario |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Converti esadecimale in binario |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Restituire un UUID |

### Valutazione dei dati {#data-evaluation}

| Funzione | Descrizione |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Restituisce il primo argomento non-null |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Restituisce un elenco di elementi non univoci |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Restituisce un set di elementi univoci |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Concatenazione |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Concatenazione con separatore |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Restituisce il conteggio totale delle righe |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Decodifica con un set di caratteri |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Restituire l&#39;input [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)th |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codifica con un set di caratteri |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Restituisce il primo valore |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Indica se una colonna è raggruppata |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Restituisce il livello di raggruppamento |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Restituisce un indice basato su 1 dell&#39;occorrenza del carattere |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Restituisce una tupla da un input JSON |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Restituisce il valore prima dell&#39;offset |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Restituisce l&#39;ultimo valore |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Restituisce i primi caratteri [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Restituisce la lunghezza della stringa |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Restituisce la distanza di Levenshtein tra le stringhe |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Restituisce la posizione della prima occorrenza di una sottostringa |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Concatenare una mappa |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Restituire le chiavi di una mappa |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Restituisce i valori di una mappa |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Dividere le righe in partizioni |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Restituisce null se true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Restituisce value se null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Restituisce il valore se non null |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Estrae parte di un URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Calcola il livello di un valore |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Estrae qualcosa che corrisponda al regex |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Sostituisce qualcosa che corrisponde al regex |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Restituisce una stringa che si ripete |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Sostituire tutte le istanze di una stringa |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Creare un rollup multidimensionale |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Assegna un numero di riga univoco |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Restituisce lo schema del JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Divide la stringa in un array di parole |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Genera un array di elementi |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Spostamento bit a sinistra con segno |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Spostamento bit a bit con segno a destra |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Spostamento bit a destra senza segno |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Restituisce la dimensione dell&#39;array |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Restituire una stringa con [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) spazi |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Dividi stringa |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Restituisce l&#39;indice della sottostringa |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Finestra |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analizzare i nodi XML |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Analizzare i nodi XML per il doppio |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analizza i nodi XML per Mobile |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analizza i nodi XML per il numero intero |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analizzare i nodi XML per long |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analizza i nodi XML per il numero intero breve |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analizza i nodi XML per la stringa |

### Informazioni correnti {#current-information}

| Funzione | Descrizione |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Restituisce il database corrente |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Restituisce la data corrente |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Restituisce la marca temporale corrente |

### Funzioni di ordine superiore {#higher-order}

| Funzione | Descrizione |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Trasformare gli elementi in un array |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Controlla se l&#39;elemento esiste |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrare l&#39;array di input |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Applicazione di un operatore binario a tutti gli elementi |