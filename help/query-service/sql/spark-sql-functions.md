---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni SQL Spark
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a10508770a862621403bad94c14db4529051020c
workflow-type: tm+mt
source-wordcount: '4996'
ht-degree: 5%

---


# [!DNL Spark] Funzioni SQL

Gli assistenti [!DNL Spark] SQL forniscono funzioni [!DNL Spark] SQL integrate per estendere le funzionalità SQL.

Riferimento: [Documentazione della funzione SQL Spark](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>Non tutte le funzioni della documentazione esterna sono supportate.

## Categorie

- [Matematica e operatori statistici e funzioni](#math)
- [Operatori logici](#logical-operators)
- [Funzioni data/ora](#datetime-functions)
- [Funzioni di aggregazione](#aggregate-functions)
- [Array](#arrays)
- [Funzioni di inserimento dati](#datatype-casting)
- [Funzioni di conversione e formattazione](#conversion)
- [Valutazione dei dati](#data-evaluation)
- [Informazioni correnti](#current-information)
- [Funzioni di ordine superiore](#higher-order)

### Matematica e operatori statistici e funzioni {#math}

#### Modulo

`expr1 % expr2`: Restituisce il resto dopo `expr1`/`expr2`.

Esempi:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Moltiplica

`expr1 * expr2`: Restituisce `expr1`*`expr2`.

Esempio:

```
> SELECT 2 * 3;
 6
```

#### Add

`expr1 + expr2`: Restituisce `expr1`+`expr2`.

Esempio:

```
> SELECT 1 + 2;
 3
```

#### Sottrai

`expr1 - expr2`: Restituisce `expr1`-`expr2`.

Esempio:

```
> SELECT 2 - 1;
 1
```

#### Dividi

`expr1 / expr2`: Restituisce `expr1`/`expr2`. Esegue sempre la divisione in virgola mobile.

Esempi:

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Restituisce il valore assoluto del valore numerico.

Esempio:

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Restituisce il coseno inverso (detto anche coseno di arco) di `expr`, come se fosse calcolato da `java.lang.Math.acos`.

Esempi:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### circa_percentile

`approx_percentile(col, percentage [, accuracy])`: Restituisce il valore percentile approssimativo della colonna numerica `col` alla percentuale specificata. Il valore della percentuale deve essere compreso tra 0,0 e 1,0. Il `accuracy` parametro (predefinito: 10000) è un letterale numerico positivo che controlla la precisione di approssimazione al costo della memoria. Più alto è il valore dei `accuracy` rendimenti più precisi, `1.0/accuracy` è l&#39;errore relativo dell&#39;approssimazione. Quando `percentage` è un array, ogni valore dell&#39;array di percentuali deve essere compreso tra 0,0 e 1,0. In questo caso, viene restituito l&#39;array percentile approssimativo della colonna `col` all&#39;array di percentuali specificato.

Esempi:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asina

`asin(expr)`: Restituisce il seno inverso (detto anche sinusoidale di arco), l&#39;arco sinusoidale di `expr`, come se fosse calcolato da `java.lang.Math.asin`.

Esempi:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Restituisce la tangente inversa (nota anche come tangente ad arco) di `expr`, come se calcolata da `java.lang.Math.atan`

Esempio:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Restituisce l&#39;angolo in radianti tra l&#39;asse x positivo di un piano e il punto dato dalle coordinate (`exprX`, `exprY`), come se fosse calcolato da `java.lang.Math.atan2`.

Argomenti:

`exprY`: Coordinata sull&#39;asse`exprX`y: Coordinata sull&#39;asse x

Esempio:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Restituisce la media calcolata dai valori di un gruppo.

#### cardinalità

`cardinality(expr)`: Restituisce la dimensione di un array o di una mappa. La funzione restituisce -1 se il relativo input è null e `spark.sql.legacy.sizeOfNull` è impostato su true (predefinito). Se `spark.sql.legacy.sizeOfNull` è impostata su false, la funzione restituisce null per l&#39;input nullo.

Esempi:

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: Restituisce la radice del cubo di `expr`.

Esempio:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Restituisce il numero intero più piccolo non più piccolo di `expr`.

Esempi:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### soffitto

`ceiling(expr)`: Restituisce il numero intero più piccolo non più piccolo di `expr`.

Esempi:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Converti `num` da `from_base` a `to_base`

Esempi:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Restituisce il coefficiente di correlazione Pearson tra un insieme di coppie di numeri.

#### cos

`cos(expr)`: Restituisce il coseno di `expr`, come se fosse calcolato da `java.lang.Math.cos`.

Esempio:

```
> SELECT cos(0);
 1.0
```

#### palude

`cosh(expr)`: Restituisce il coseno iperbolico di `expr`, come se fosse calcolato da `java.lang.Math.cosh`.

Argomenti:
- `expr`: Angolo iperbolico

Esempio:

```
> SELECT cosh(0);
 1.0
```

#### culla

`cot(expr)`: Restituisce la cotangente di `expr`, come se fosse calcolata da `1/java.lang.Math.cot`.

Argomenti:
- `expr`: Angolo in radianti

Esempio:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Calcola il grado di un valore in un gruppo di valori. Il risultato è uno più il valore di classifica precedentemente assegnato. A differenza della funzione `rank`, `dense_rank` non crea spazi nella sequenza di classifica.

#### e

`e()`: Restituisce il numero di Eulero, e.

Esempio:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Restituisce e alla potenza di `expr`.

Esempio:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Restituisce exp(`expr`) - 1.

Esempio:

```
> SELECT expm1(0);
 0.0
```

#### fattoriale

`factorial(expr)`: Restituisce il fattoriale di `expr`. `expr` è [0.20]. In caso contrario, null.

Esempio:

```
> SELECT factorial(5);
 120
```

#### pavimento

`floor(expr)`: Restituisce il numero intero più grande non maggiore di `expr`.

Esempi:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### massimo

`greatest(expr, ...)`: Restituisce il valore massimo di tutti i parametri, ignorando i valori null.

Esempio:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypot

`hypot(expr1, expr2)`: Restituisce sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Esempio:

```
> SELECT hypot(3, 4);
 5.0
```

#### curtosi

`kurtosis(expr)`: Restituisce il valore della curtosi calcolato in base ai valori di un gruppo.


#### minimo

`least(expr, ...)`: Restituisce il valore minimo di tutti i parametri, ignorando i valori null.

Esempio:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`: Restituisce la distanza di Levenshtein tra le due stringhe specificate.

Esempi:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Restituisce il logaritmo naturale (base e) di `expr`.

Esempio:

```
> SELECT ln(1);
 0.0
```

#### log

`log(base, expr)`: Restituisce il logaritmo di `expr` con `base`.

Esempio:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Restituisce il logaritmo di `expr` con base 10.

Esempio:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Restituisce `log(1 + expr)`.

Esempio:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Restituisce il logaritmo di `expr` con base 2.

Esempio:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Restituisce il valore massimo di `expr`.

#### medium

`mean(expr)`: Restituisce la media calcolata dai valori di un gruppo.

#### min

`min(expr)`: Restituisce il valore minimo di `expr`.

#### monotonicamente_increase_id

`monotonically_increasing_id()`: Restituisce numeri interi a 64 bit in aumento monotonico. L’ID generato è garantito in modo monotonico crescente e univoco, ma non consecutivo. L&#39;implementazione corrente inserisce l&#39;ID della partizione nei 31 bit superiori, mentre i 33 bit inferiori rappresentano il numero di record all&#39;interno di ogni partizione. Il presupposto è che la cornice dati ha meno di 1 miliardo di partizioni, e ogni partizione ha meno di 8 miliardi di record. La funzione non è deterministica perché il risultato dipende dagli ID della partizione.

#### negativo

`negative(expr)`: Restituisce il valore negativo di `expr`.

Esempio:

```
> SELECT negative(1);
 -1
```

#### percentuale_rank

`percent_rank()`: Calcola la classificazione percentuale di un valore in un gruppo di valori.

#### percentile

`percentile(col, percentage [, frequency])`: Restituisce il valore percentile esatto della colonna numerica `col` alla percentuale specificata. Il valore di `percentage` deve essere compreso tra 0,0 e 1,0. Il valore di `frequency` dovrebbe essere integrale positivo.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Restituisce l&#39;array di valori percentili esatti della colonna numerica `col` in corrispondenza delle percentuali specificate. Ogni valore dell&#39;array di percentuali deve essere compreso tra 0,0 e 1,0. Il valore di `frequency` dovrebbe essere integrale positivo.

#### percentile_circa

`percentile_approx(col, percentage [, accuracy])`: Restituisce il valore percentile approssimativo della colonna numerica `col` alla percentuale specificata. Il valore di `percentage` deve essere compreso tra 0,0 e 1,0. Il `accuracy` parametro (predefinito: 10000) è un letterale numerico positivo che controlla la precisione di approssimazione al costo della memoria. Più alto è il valore dei `accuracy` rendimenti più precisi, `1.0/accuracy` è l&#39;errore relativo dell&#39;approssimazione. Quando `percentage` è un array, ogni valore dell&#39;array di percentuali deve essere compreso tra 0,0 e 1,0. In questo caso, restituisce l&#39;array percentile approssimativo di colonna `col` alla matrice percentuale specificata.

Esempi:

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Restituisce pi.

Esempio:

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Restituisce il valore positivo di `expr1` mod `expr2`.

Esempi:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positivo

`positive(expr)`: Restituisce il valore positivo di `expr`

#### zuppa

`pow(expr1, expr2)`: Aumenta `expr1` al potere di `expr2`.

Esempio:

```
> SELECT pow(2, 3);
 8.0
```

#### alimentazione

`power(expr1, expr2)`: Aumenta `expr1` al potere di `expr2`.

Esempi:

```
> SELECT power(2, 3);
 8.0
```

#### radianti

`radians(expr)`: Converte i gradi in radianti.

Argomenti:

- `expr`: Angolo in gradi

Esempio:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Restituisce un valore casuale con valori distribuiti in modo indipendente e identico (i.i.d.) in modo uniforme in (0, 1).

Esempi:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>Questa funzione non è deterministica in generale.

#### randn

`randn([seed])`: Restituisce un valore casuale con valori indipendenti e distribuiti in modo identico (i.i.d.) provenienti dalla distribuzione normale standard.

Esempi:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>Questa funzione non è deterministica in generale.

#### rint

`rint(expr)`: Restituisce il valore doppio più vicino in valore all&#39;argomento ed è uguale a un numero intero matematico.

Esempi:

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: Restituisce `expr` arrotondato a `d` posizioni decimali utilizzando la modalità di arrotondamento HALF_UP.

Esempio:

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`: Restituisce -1,0, 0,0 o 1,0 come `expr` negativo, 0 o positivo.

Esempio:

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: Restituisce -1,0, 0,0 o 1,0 come `expr` negativo, 0 o positivo.

Esempio:

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Restituisce il seno di `expr`, come se fosse calcolato da `java.lang.Math.sin`.

Argomenti:

- `expr`: Angolo in radianti

Esempio:

```
> SELECT sin(0);
 0.0
```

#### pecora

`sinh(expr)`: Restituisce un seno iperbolico di `expr`, come se fosse calcolato da `java.lang.Math.sinh`.

Argomenti:

- `expr`: Angolo iperbolico

Esempio:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Restituisce la radice quadrata di `expr`.

Esempio:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Restituisce la deviazione standard del campione calcolata dai valori di un gruppo.

#### stddev_pop

`sttdev_pop(expr)`: Restituisce la deviazione standard della popolazione calcolata dai valori di un gruppo.

#### stddev_samp

`stddev_samp(expr)`: Restituisce la deviazione standard del campione calcolata dai valori di un gruppo.

#### sum

`sum(expr)`: Restituisce la somma calcolata dai valori di un gruppo.

#### abbronzatura

`tan(expr)`: Restituisce la tangente di `expr`, come se calcolata da `java.lang.Math.tan`.

Argomenti:

- `expr`: Angolo in radianti

Esempio:

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Restituisce la tangente iperbolica di `expr`, come se fosse calcolata da `java.lang.Math.tanh`.

Argomenti:

- `expr`: Angolo iperbolico

Esempio:

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Restituisce la varianza della popolazione calcolata in base ai valori di un gruppo.

#### Var_samp

`var_samp(expr)`: Restituisce la varianza del campione calcolata dai valori di un gruppo.

#### varianza

`variance(expr)`: Restituisce la varianza del campione calcolata dai valori di un gruppo.

### Operatori logici {#logical-operators}

#### Not logico

`! expr`: Not logico.

#### Minore di

`expr1 < expr2`: Restituisce true se `expr1` è minore di `expr2`.

Argomenti:

- `expr1, expr2`: Le due espressioni devono essere dello stesso tipo oppure possono essere inserite in un tipo comune e devono essere un tipo che può essere ordinato. Ad esempio, il tipo di mappa non è ordinabile, quindi non è supportato. Per tipi complessi, ad esempio matrice/struttura, i tipi di dati dei campi devono essere ordinabili.

Esempi:

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Minore o uguale a

`expr1 <= expr2`: Restituisce true se `expr1` è minore o uguale a `expr2`.

Argomenti:

- `expr1, expr2`: Le due espressioni devono essere dello stesso tipo o possono essere collegate a un tipo comune e devono essere un tipo che può essere ordinato. Ad esempio, il tipo di mappa non è ordinabile, quindi non è supportato. Per tipi complessi come array/struttura, i tipi di dati dei campi devono essere ordinabili.

Esempi:

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Uguale a

`expr1 = expr2`: Restituisce true se `expr1` è uguale a `expr2`, oppure false in caso contrario.

Argomenti:

- `expr1, expr2`: Le due espressioni devono essere dello stesso tipo oppure possono essere inserite in un tipo comune e devono essere un tipo che può essere utilizzato per il confronto di uguaglianza. Il tipo di mappa non è supportato. Per tipi complessi, ad esempio matrice/struttura, i tipi di dati dei campi devono essere ordinabili.

Esempi:

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Maggiore di

`expr1 > expr2`: Restituisce true se `expr1` è maggiore di `expr2`.

Argomenti:

- `expr1, expr2`: Le due espressioni devono essere dello stesso tipo oppure possono essere inserite in un tipo comune e devono essere un tipo che può essere ordinato. Ad esempio, il tipo di mappa non è ordinabile, quindi non è supportato. Per tipi complessi, ad esempio matrice/struttura, i tipi di dati dei campi devono essere ordinabili.

Esempi:

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Maggiore o uguale a

`expr1 >= expr2`: Restituisce true se `expr1` è maggiore o uguale a `expr2`.

Argomenti:

- `expr1, expr2`: Le due espressioni devono essere dello stesso tipo oppure possono essere inserite in un tipo comune e devono essere un tipo che può essere ordinato. Ad esempio, il tipo di mappa non è ordinabile, quindi non è supportato. Per tipi complessi, ad esempio matrice/struttura, i tipi di dati dei campi devono essere ordinabili.

Esempi:

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitwise esclusive o

`expr1 ^ expr2`: Restituisce il risultato di OR bit a bit esclusivo di `expr1` e `expr2`.

Esempio:

```
> SELECT 3 ^ 5;
 2
```

#### e

`expr1 and expr2`: AND logico.

#### array_Sovrapposizione

`arrays_overlap(a1, a2)`: Restituisce true se un1 contiene almeno un elemento non-null presente anche in a2. Se le matrici non hanno un elemento comune e non sono entrambe vuote e una di esse contiene un elemento null, viene restituito null. In caso contrario, viene restituito false.

Esempio:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Dal: 2.4.0

#### assert_true

`assert_true(expr)`: Genera un&#39;eccezione se `expr` non è vera.

Esempio:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Se `expr1` restituisce true, restituisce `expr2`; altrimenti restituisce `expr3`.

Esempio:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Restituisce `expr2` se `expr1` è null o `expr1` in caso contrario.

Esempio:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Restituisce true se `expr` è uguale a qualsiasi valore valN.

Argomenti:
- `expr1, expr2, expr3, ...`: Gli argomenti devono essere dello stesso tipo.

Esempi:

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: Restituisce true se `expr` è NaN o false in caso contrario.

Esempio:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Restituisce true se non `expr` è null o false in caso contrario.

Esempi:

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: Restituisce true se `expr` è null o false in caso contrario.

Esempio:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Restituisce `expr1` se non è NaN o `expr2` in altro modo.

Esempio:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Not logico.

#### o

`expr1 or expr2`: OR logico.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Restituisce true se l&#39;espressione XPath restituisce true o se viene trovato un nodo corrispondente.

Esempio:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Funzioni data/ora {#datetime-functions}

#### add_month

`add_months(start_date, num_months)`: Restituisce la data `num_months` successiva a `start_date`.

Esempio:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Dal: 1,5,0

#### date_add

`date_add(start_date, num_days)`: Restituisce la data `num_days` successiva a `start_date`.

Esempio:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Dal: 1,5,0

#### date_format

`date_format(timestamp, fmt)`: Effettua la conversione `timestamp` in un valore di stringa nel formato specificato dal formato data `fmt`.

Esempio:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Dal: 1,5,0

#### date_sub

`date_sub(start_date, num_days)`: Restituisce la data `num_days` precedente `start_date`.

Esempio:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Dal: 1,5,0

#### date_trunc

`date_trunc(fmt, ts)`: Restituisce le marche temporali troncate all&#39;unità specificata dal modello di formato `fmt`. `fmt` Deve essere uno di [&quot;ANNO&quot;, &quot;AAAA&quot;, &quot;AA&quot;, &quot;MON&quot;, &quot;MESE&quot;, &quot;MM&quot;, &quot;GIORNO&quot;, &quot;GG&quot;, &quot;ORA&quot;, &quot;MINUTO&quot;, &quot;SECONDO&quot;, &quot;SETTIMANA&quot;, &quot;TRIMESTRE&quot;]

Esempi:

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Dal: 2.3.0

#### datediff

`datediff(endDate, startDate)`: Restituisce il numero di giorni da `startDate` a `endDate`.

Esempi:

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Dal: 1,5,0

#### giorno

`day(date)`: Restituisce il giorno del mese della data/marca temporale.

Esempio:

```
> SELECT day('2009-07-30');
 30
```

Dal: 1,5,0

#### giorno di mese

`dayofmonth(date)`: Restituisce il giorno del mese della data/marca temporale.

Esempio:

```
> SELECT dayofmonth('2009-07-30');
 30
```

Dal: 1,5,0

#### giorno della settimana

`dayofweek(date)`: Restituisce il giorno della settimana per data/marca temporale (1 = domenica, 2 = lunedì, ..., 7 = sabato).

Esempio:

```
> SELECT dayofweek('2009-07-30');
 5
```

Dal: 2.3.0

#### giorno dell&#39;anno

`dayofyear(date)`: Restituisce il giorno dell’anno della data/marca temporale.

Esempio:

```
> SELECT dayofyear('2016-04-09');
 100
```

Dal: 1,5,0

#### from_unixtime

`from_unixtime(unix_time, format)`: Restituisce `unix_time` il valore specificato `format`.

Esempio:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Dal: 1,5,0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interpreta una marca temporale come &#39;2017-07-14 02:40:00.0&#39; come ora in UTC, e la riproduce come marca temporale nel fuso orario specificato. Ad esempio, &#39;GMT+1&#39; restituirebbe &#39;2017-07-14 03:40:00.0&#39;.

Esempio:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Dal: 1,5,0

#### ora

`hour(timestamp)`: Restituisce il componente ora della stringa/marca temporale.

Esempio:

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Dal: 1,5,0

#### last_day

`last_day(date):` Restituisce l&#39;ultimo giorno del mese a cui la data appartiene.

Esempio:

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Dal: 1,5,0

#### minuto

`minute(timestamp)`: Restituisce il componente minuto della stringa/marca temporale.

Esempio:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Dal: 1,5,0

#### mese

`month(date)` Restituisce il componente del mese della data/marca temporale.

Esempio:

```
> SELECT month('2016-07-30');
 7
```

Dal: 1,5,0

#### mesi_between

`months_between(timestamp1, timestamp2[, roundOff])`: Se `timestamp1` è successiva a `timestamp2`, il risultato è positivo. Se `timestamp1` e `timestamp2` lo stesso giorno del mese, o se entrambi sono l&#39;ultimo giorno del mese, l&#39;ora del giorno verrà ignorata. In caso contrario, la differenza viene calcolata in base a 31 giorni al mese e arrotondata a 8 cifre a meno che `roundOff=false`.

Esempi:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Dal: 1,5,0

#### next_day

`next_day(start_date, day_of_week)`: Restituisce la prima data successiva a quella indicata `start_date` e denominata come indicato.

Esempio:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Dal: 1,5,0

#### trimestre

`quarter(date)`: Restituisce il trimestre dell&#39;anno per la data, compreso tra 1 e 4.

Esempio:

```
> SELECT quarter('2016-08-31');
 3
```

Dal: 1,5,0

#### secondo

`second(timestamp)`: Restituisce il secondo componente della stringa/marca temporale.

Esempio:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Dal: 1,5,0

#### to_date

`to_date(date_str[, fmt])`: Analizza l&#39; `date_str` espressione con l&#39; `fmt` espressione fino a una data. Restituisce null con input non valido. Per impostazione predefinita, segue le regole di inserimento a una data se l&#39;oggetto `fmt` viene omesso.

Esempi:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Dal: 1,5,0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Analizza l&#39; `timestamp` espressione con l&#39; `fmt` espressione su una marca temporale. Restituisce null con input non valido. Per impostazione predefinita, segue le regole di inserimento in una marca temporale se `fmt` viene omessa.

Esempi:

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Dal: 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Restituisce la marca temporale UNIX dell&#39;ora specificata.

Esempio:

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Dal: 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Interpreta una marca temporale come &#39;2017-07-14 02:40:00.0&#39; come un&#39;ora nel fuso orario specificato e la visualizza come marca temporale in UTC. Ad esempio, &#39;GMT+1&#39; restituirebbe &#39;2017-07-14 01:40:00.0&#39;.

Esempio:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Dal: 1,5,0

#### trunc

`trunc(date, fmt)`: Restituisce la data con la parte temporale del giorno troncata all&#39;unità specificata dal modello di formato `fmt`. `fmt` è uno di [&quot;anno&quot;, &quot;aaaa&quot;, &quot;yy&quot;, &quot;mon&quot;, &quot;mese&quot;, &quot;mm&quot;]

Esempi:

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Dal: 1,5,0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Restituisce la marca temporale UNIX dell&#39;ora corrente o specificata.

Esempi:

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Dal: 1,5,0

#### giorno feriale

`weekday(date)`: Restituisce il giorno della settimana per data/marca temporale (0 = lunedì, 1 = martedì, ..., 6 = domenica).

Esempio:

```
> SELECT weekday('2009-07-30');
 3
```

Dal: 2.4.0

#### week_of_year

`weekofyear(date)`: Restituisce la settimana dell&#39;anno della data specificata. Una settimana inizia il lunedì e la settimana 1 è la prima settimana con >3 giorni.

Esempio:

```
> SELECT weekofyear('2008-02-20');
 8
```

Dal: 1,5,0

#### quando

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Quando `expr1` = true, restituisce `expr2`; else quando `expr3` = true, restituisce `expr4`; altrimenti restituisce `expr5`.

Argomenti:

- `expr1`, `expr3`: Le espressioni di condizione del ramo devono essere di tipo booleano.
- `expr2`, `expr4`, `expr5`: Le espressioni del valore del ramo e dell&#39;espressione del valore else devono essere dello stesso tipo o essere coerenti con un tipo comune.

Esempi:

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### anno

`year(date)`: Restituisce il componente dell’anno della marca data/ora.

Esempio:

```
> SELECT year('2016-07-30');
 2016
```

Dal: 1,5,0

### Funzioni di aggregazione {#aggregate-functions}

#### approssimx_count_distinta

`approx_count_distinct(expr[, relativeSD])`: Restituisce la cardinalità stimata da HyperLogLog++. `relativeSD` definisce l&#39;errore massimo di stima consentito.

### Array {#arrays}

#### array

`array(expr, ...)`: Restituisce un array con gli elementi specificati.

Esempio:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Restituisce true se la matrice contiene il valore.

Esempio:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinta

`array_distinct(array)`: Rimuove i valori duplicati dall&#39;array.

Esempio:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Dal: 2.4.0

#### array_exception

`array_except(array1, array2)`: Restituisce un array degli elementi in `array1` ma non in `array2`, senza duplicati.

Esempio:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Dal: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Restituisce un array degli elementi nell&#39;intersezione di `array1` e `array2`, senza duplicati.

Esempio:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Dal: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Concatena gli elementi dell&#39;array specificato utilizzando il delimitatore e una stringa opzionale per sostituire i valori Null. Se non viene impostato alcun valore, `nullReplacement`qualsiasi valore nullo viene filtrato.

Esempi:

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Dal: 2.4.0

#### array_max

`array_max(array)`: Restituisce il valore massimo nell&#39;array. Gli elementi Null vengono ignorati.

Esempio:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Dal: 2.4.0

#### array_min

`array_min(array)`: Restituisce il valore minimo nell&#39;array. Gli elementi Null vengono ignorati.

Esempio:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Dal: 2.4.0

#### array_position

`array_position(array, element)`: Restituisce l&#39;indice (basato su 1) del primo elemento dell&#39;array per il periodo di tempo.

Esempio:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Dal: 2.4.0

#### array_remove

`array_remove(array, element)`: Rimuovete dall&#39;array tutti gli elementi uguali all&#39;elemento.

Esempio:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Dal: 2.4.0

#### array_repeat

`array_repeat(element, count)`: Restituisce l&#39;array contenente le ore di conteggio degli elementi.

Esempio:

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Dal: 2.4.0

#### array_sort

`array_sort(array)`: Ordina l&#39;array di input in ordine crescente. Gli elementi dell&#39;array di input devono essere ordinabili. Gli elementi Null vengono inseriti alla fine dell&#39;array restituito.

Esempio:

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Dal: 2.4.0

#### array_union

`array_union(array1, array2)`: Restituisce un array degli elementi nell&#39;unione di `array1` e `array2`, senza duplicati.

Esempio:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Dal: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Restituisce un array unito di strutture in cui la struttura N contiene tutti i valori N-th degli array di input.

Esempi:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Dal: 2.4.0

#### element_at

`element_at(array, index)`: Restituisce l&#39;elemento dell&#39;array in corrispondenza dell&#39;indice specificato (basato su 1). Se `index < 0`, accede agli elementi dall&#39;ultimo al primo. Restituisce NULL se l&#39;indice supera la lunghezza dell&#39;array.

`element_at(map, key)`: Restituisce il valore per la chiave specificata, o NULL se la chiave non è contenuta nella mappa

Esempi:

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Dal: 2.4.0

#### esplodere

`explode(expr)`: Separa gli elementi della matrice `expr` in più righe o gli elementi della mappa `expr` in più righe e colonne.

Esempi:

```
> SELECT explode(array(10, 20));
 10
 20
```

#### esplode_external

`explode_outer(expr)`: Separa gli elementi della matrice `expr` in più righe o gli elementi della mappa `expr` in più righe e colonne.

Esempio:

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Restituisce l&#39;indice (basato su 1) della stringa specificata (`str`) nell&#39;elenco delimitato da virgole (`str_array`). Restituisce 0, se la stringa non è stata trovata o se la stringa specificata (`str`) contiene una virgola.

Esempio:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### appiattire

`flatten(arrayOfArrays)`: Trasforma un array di array in un singolo array.

Esempio:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Dal: 2.4.0

#### inline

`inline(expr)`: Consente di esplodere un array di strutture in una tabella.

Esempio:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_external

`inline_outer(expr)`: Consente di esplodere un array di strutture in una tabella.

Esempio:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### post-esploso

`posexplode(expr)`: Separa gli elementi della matrice `expr` in più righe con posizioni, o gli elementi della mappa `expr` in più righe e colonne con posizioni.

Esempio:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posesplode_external

`posexplode_outer(expr)`: Separa gli elementi della matrice `expr` in più righe con posizioni, o gli elementi della mappa `expr` in più righe e colonne con posizioni.

Esempio:

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### reverse

`reverse(array)`: Restituisce una stringa inversa o un array con ordine inverso degli elementi.

Esempi:

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Dal: 1,5,0
>[!NOTE]
>
>La logica rse per gli array è disponibile dal 2.4.0.

#### mescolare

`shuffle(array)`: Restituisce una permutazione casuale dell&#39;array specificato.

Esempi:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Dal: 2.4.0
>[!NOTE]
>
>è non deterministica.

#### fetta

`slice(x, start, length)`: L&#39;array dei sottoinsiemi x inizia dall&#39;inizio dell&#39;indice (o inizia dalla fine se l&#39;inizio è negativo) con la lunghezza specificata.

Esempi:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Dal: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Dispone l&#39;array di input in ordine crescente o decrescente in base all&#39;ordine naturale degli elementi dell&#39;array. Gli elementi Null vengono inseriti all&#39;inizio dell&#39;array restituito in ordine crescente o alla fine dell&#39;array restituito in ordine decrescente.

Esempi:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Unisce i due array, a livello di elemento, in un singolo array utilizzando la funzione. Se una matrice è più corta, alla fine vengono aggiunti dei valori null che corrispondono alla lunghezza della matrice più lunga, prima di applicare la funzione.

Esempi:

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Dal: 2.4.0

### Funzioni di inserimento dati {#datatype-casting}

#### bigotto

`bigint(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `bigint`.

#### binary

`binary(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `binary`.

#### booleano

`boolean(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `boolean`.

#### cast

`cast(expr AS type)`: Crea il valore `expr` in base al tipo di dati di destinazione `type`.

Esempio:

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `date`.

#### decimal

`decimal(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `decimal`.

#### double

`double(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `double`.

#### float

`float(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `float`.

#### int

`int(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `int`.

#### map

`map(key0, value0, key1, value1, ...)`: Crea una mappa con le coppie chiave/valore specificate.

Esempio:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### piccolo

`smallint(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Crea una mappa dopo la divisione del testo in coppie chiave/valore utilizzando i delimitatori. I delimitatori predefiniti sono &#39;,&#39; per `pairDelim` e &#39;:&#39; per `keyValueDelim`.

Esempi:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `string`.

#### struct

`struct(col1, col2, col3, ...)`: Crea una struttura con i valori dei campi specificati.

#### tinyint

`tinyint(expr)`: Crea il valore `expr` in base al tipo di dati di destinazione `tinyint`.

### Funzioni di conversione e formattazione {#conversion}

#### ascii

`ascii(str)`: Restituisce il valore numerico del primo carattere di `str`.

Esempi:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Converte l&#39;argomento da un binario `bin` a una stringa base 64.

Esempio:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Restituisce la rappresentazione in formato stringa del valore lungo `expr` rappresentato in binario.

Esempi:

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: Restituisce la lunghezza in bit dei dati stringa o il numero di bit dei dati binari.

Esempio:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Restituisce il carattere ASCII con l&#39;equivalente binario del `expr`. Se n è maggiore di 256, il risultato è equivalente a `chr(n % 256)`.

Esempio:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Restituisce la lunghezza del carattere dei dati stringa o il numero di byte di dati binari. La lunghezza dei dati stringa include gli spazi finali. La lunghezza dei dati binari include zeri binari.

Esempi:

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### caratteri_length

`character_length(expr)`: Restituisce la lunghezza del carattere dei dati stringa o il numero di byte di dati binari. La lunghezza dei dati stringa include gli spazi finali. La lunghezza dei dati binari include zeri binari.

Esempi:

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: Restituisce il carattere ASCII con l&#39;equivalente binario di expr. Se n è maggiore di 256, il risultato è equivalente a `chr(n % 256)`

Esempio:

```
> SELECT chr(65);
 A
```

#### gradi

`degrees(expr)`: Converte i radianti in gradi.

Argomenti:
- `expr`: Angolo in radianti

Esempio:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formatta il numero `expr1` come &#39;#,###,###.##&#39;, arrotondato a `expr2` cifre decimali. Se `expr2` è 0, il risultato non ha separatori decimali o parti frazionarie. `expr2` accetta anche un formato specificato dall&#39;utente. Questo è destinato a funzionare come MySQL `FORMAT`.

Esempi:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Restituisce un valore struct con il valore specificato `jsonStr` e `schema`.

Esempi:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Dal: 2.2.0

#### hash

`hash(expr1, expr2, ...)`: Restituisce un valore hash degli argomenti.

Esempio:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### eccitare

`hex(expr)`: Effettua la conversione `expr` in esadecimale.

Esempi:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Restituisce `str` la prima lettera di ciascuna parola in caratteri maiuscoli. Tutte le altre lettere sono in lettere minuscole. Le parole sono delimitate da uno spazio vuoto.

Esempio:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### custodia

`lcase(str)`: Restituisce `str` con tutti i caratteri modificati in caratteri minuscoli.

Esempio:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### Lower

`lower(str)`: Restituisce `str` con tutti i caratteri modificati in caratteri minuscoli.

Esempio:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Restituisce `str`, con `pad` aggiunta a sinistra a una lunghezza di `len`. Se `str` è più lungo di `len`, il valore restituito è ridotto a `len` caratteri.

Esempi:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Crea una mappa con le coppie chiave/valore specificate.

Esempio:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_array

`map_from_arrays(keys, values)`: Crea una mappa con una coppia di array chiave/valore specificati. Gli elementi nelle chiavi non possono essere null.

Esempio:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Dal: 2.4.0

#### map_from_entry

`map_from_entries(arrayOfEntries)`: Restituisce una mappa creata dall&#39;array specificato di voci.

Esempio:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Dal: 2.4.0

#### md5

`md5(expr)`: Restituisce un checksum MD5 a 128 bit come stringa esadecimale di `expr`.

Esempio:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### pad

`rpad(str, len, pad)`: Restituisce `str`, imbottito a destra con `pad` una lunghezza di `len`. Se `str` è più lungo di `len`, il valore restituito è ridotto a `len` caratteri.

Esempi:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Rimuove gli spazi vuoti finali da `str`.

`rtrim(trimStr, str)`: Rimuove dalla `str`stringa finale la stringa che contiene i caratteri della stringa di rifilo.

Argomenti:
- `str`: Espressione stringa
- `trimStr`: I caratteri stringa di rifilo da tagliare. Il valore predefinito è un singolo spazio

Esempi:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Restituisce un valore `sha1` hash come stringa esadecimale dell&#39;oggetto `expr`.

Esempio:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Restituisce un valore `sha1` hash come stringa esadecimale dell&#39;oggetto `expr`.

Esempio:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Restituisce un checksum della famiglia SHA-2 come stringa esadecimale di `expr`. Sono supportati SHA-224, SHA-256, SHA-384 e SHA-512. La lunghezza del bit pari a 0 equivale a 256.

Esempio:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Restituisce il codice Soundex della stringa.

Esempio:

```
> SELECT soundex('Miller');
 M460
```

#### stack

`stack(n, expr1, ..., exprk)`: Separa `expr1`, ..., `exprk` in `n` righe.

Esempio:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Restituisce la sottostringa di `str` che inizia da `pos` ed è di lunghezza `len`, oppure la sezione di matrice di byte che inizia da `pos` ed è di lunghezza `len`.

Esempi:

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### substring

`substring(str, pos[, len])`: Restituisce la sottostringa di `str` che inizia da `pos` ed è di lunghezza `len`, oppure la sezione di matrice di byte che inizia da `pos` ed è di lunghezza `len`.

Esempi:

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: Restituisce una stringa JSON con un valore di struttura specificato.

Esempi:

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Dal: 2.2.0

#### translate

`translate(input, from, to)`: Traduce la `input` stringa sostituendo i caratteri presenti nella `from` stringa con i caratteri corrispondenti nella `to` stringa.

Esempio:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: Rimuove gli spazi iniziali e finali da `str`.

`trim(BOTH trimStr FROM str)`: Rimuovere i `trimStr` caratteri iniziali e finali da `str`.

`trim(LEADING trimStr FROM str)`: Rimuovere i `trimStr` caratteri iniziali da `str`.

`trim(TRAILING trimStr FROM str)`: Rimuovere i `trimStr` caratteri finali da `str`.

Argomenti:
- `str`: Espressione stringa
- `trimStr`: I caratteri stringa di rifilo da tagliare, il valore predefinito è un singolo spazio
- `BOTH`, `FROM`: Si tratta di parole chiave per specificare il taglio dei caratteri stringa da entrambe le estremità della stringa
- `LEADING`, `FROM`: Si tratta di parole chiave per specificare il taglio dei caratteri stringa dall&#39;estremità sinistra della stringa
- `TRAILING`, `FROM`: Si tratta di parole chiave per specificare il taglio dei caratteri stringa dall&#39;estremità destra della stringa

Esempi:

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`: Restituisce `str` con tutti i caratteri modificati in caratteri maiuscoli.

Esempio:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Converte l&#39;argomento da una stringa base 64 `str` in un binario.

Esempio:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Converte l&#39;esadecimale `expr` in binario.

Esempio:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### top

`upper(str)`: Restituisce `str` con tutti i caratteri modificati in caratteri maiuscoli.

Esempio:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Restituisce una stringa di identificatore universale univoco (UUID). Il valore viene restituito come stringa canonica UUID a 36 caratteri.

Esempio:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>La funzione non è deterministica.

### Valutazione dei dati {#data-evaluation}

#### fondersi

`coalesce(expr1, expr2, ...)`: Restituisce il primo argomento non-null, se esistente. In caso contrario, null.

Esempio:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`: Raccoglie e restituisce un elenco di elementi non univoci.

#### collect_set

`collect_set(expr)`: Raccoglie e restituisce un set di elementi univoci.

#### concat

`concat(col1, col2, ..., colN)`: Restituisce la concatenazione di col1, col2, ..., colN.

Esempi:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` logica per gli array è disponibile dal 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Restituisce la concatenazione delle stringhe separate da `sep`.

Esempio:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: Restituisce il numero totale di righe recuperate, incluse le righe contenenti null.

`count(expr[, expr...])`: Restituisce il numero di righe per le quali le espressioni fornite sono tutte non-null.

`count(DISTINCT expr[, expr...])`: Restituisce il numero di righe per le quali le espressioni fornite sono univoche e non-null.

#### crc32

`crc32(expr)`: Restituisce un valore di controllo della ridondanza ciclica dell&#39;elemento `expr` bigint.

Esempio:

```
> SELECT crc32('Spark');
 1557323817
```

#### decodificare

`decode(bin, charset)`: Decodifica il primo argomento utilizzando il secondo insieme di caratteri argomento.

Esempio:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Restituisce il `n`nono input, ad esempio, restituisce `input2` se `n` è 2.

Esempio:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### codificare

`encode(str, charset)`: Codifica il primo argomento utilizzando il secondo insieme di caratteri argomento.

Esempio:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Restituisce il primo valore di `expr` per un gruppo di righe. Se `isIgnoreNull` è true, restituisce solo valori non-null.

#### first_value

`first_value(expr[, isIgnoreNull])`: Restituisce il primo valore di `expr` per un gruppo di righe. Se `isIgnoreNull` è true, restituisce solo valori non-null.

#### get_json_object

`get_json_object(json_txt, path)`: Estrae un oggetto json da `path`.

Esempio:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### group

<!-- was blank --->

#### group_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Restituisce l&#39;indice (basato su 1) della prima occorrenza di `substr` in `str`.

Esempio:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Restituisce una tupla come la funzione `get_json_object`, ma richiede più nomi. Tutti i parametri di input e i tipi di colonna di output sono stringhe.

Esempio:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])`: Restituisce il valore di `input` nella `offset`terza riga prima della riga corrente nella finestra. Il valore predefinito di `offset` è 1 e il valore predefinito di `default` è null. Se il valore di `input` at the `offset`th row è null, viene restituito null. Se non è presente una riga di offset (ad esempio, se l&#39;offset è 1, la prima riga della finestra non ha una riga precedente) e `default` viene restituita.

#### last

`last(expr[, isIgnoreNull])`: Restituisce l&#39;ultimo valore di `expr` per un gruppo di righe. Se `isIgnoreNull` è true, restituisce solo valori non-null.

#### last_value

`last_value(expr[, isIgnoreNull])`: Restituisce l&#39;ultimo valore di `expr` per un gruppo di righe. Se `isIgnoreNull` è true, restituisce solo valori non-null.

#### lead

`lead(input[, offset[, default]])`: Restituisce il valore di `input` nella `offset`terza riga dopo la riga corrente nella finestra. Il valore predefinito di `offset` è 1 e il valore predefinito di `default` è null. Se il valore di `input` at the `offset`th row è null, viene restituito null. Se non è presente una riga di offset (ad esempio, se l&#39;offset è 1, l&#39;ultima riga della finestra non ha alcuna riga successiva) e `default` viene restituita.


#### left

`left(str, len)`: Restituisce i caratteri più a sinistra `len` (`len` può essere di tipo stringa) della stringa `str`. Se `len` è minore o uguale a 0, il risultato è una stringa vuota.

Esempio:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Restituisce la lunghezza del carattere dei dati stringa o il numero di byte di dati binari. La lunghezza dei dati stringa include gli spazi finali. La lunghezza dei dati binari include zeri binari.

Esempi:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### locate

`locate(substr, str[, pos])`: Restituisce la posizione della prima occorrenza di `substr` in `str` dopo la posizione `pos`. Il valore specificato `pos` e restituito sono basati su 1.

Esempi:

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: Restituisce l&#39;unione di tutte le mappe specificate.

Esempio:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Dal: 2.4.0

#### map_keys

`map_keys(map)`: Restituisce un array non ordinato contenente le chiavi della mappa.

Esempio:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Restituisce un array non ordinato contenente i valori della mappa.

Esempio:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### nitido

`ntile(n)`: Divide le righe per ogni partizione della finestra in `n` bucket che vanno da 1 al massimo `n`.

#### nullif

`nullif(expr1, expr2)`: Restituisce null se `expr1` è uguale a `expr2`oppure `expr1` altrimenti.

Esempio:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Restituisce `expr2` se `expr1` è null o `expr1` in caso contrario.

Esempio:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Restituisce `expr2` se `expr1` non è null o `expr3` in caso contrario.

Esempio:

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Estrae una parte da un URL.

Esempi:

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`: Restituisce la posizione della prima occorrenza di `substr` in `str` dopo la posizione `pos`. Il valore specificato `pos` e restituito sono basati su 1.

Esempi:

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### rank

`rank()`: Calcola il grado di un valore in un gruppo di valori. Il risultato è uno più il numero di righe precedenti o uguali alla riga corrente nell&#39;ordine della partizione. I valori producono spazi vuoti nella sequenza.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Estrae un gruppo che corrisponde a `regexp`.

Esempio:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Sostituisce tutte le sottostringhe di `str` cui corrisponde `regexp` a `rep`.

Esempio:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repeat

`repeat(str, n)`: Restituisce la stringa che ripete il valore stringa specificato in ore.

Esempio:

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: Sostituisce tutte le occorrenze di `search` con `replace`.

Argomenti:
- `str`: Espressione stringa
- `search`: Un&#39;espressione stringa. Se non `search` viene trovata in `str`, `str` viene restituita invariata.
- `replace`: Un&#39;espressione stringa. Se non `replace` è specificata o è una stringa vuota, nulla sostituisce la stringa rimossa da `str`.

Esempio:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### rollup

<!-- was blank -->

#### row_number

`row_number()`: Assegna un numero sequenziale univoco a ogni riga, a partire da una, in base all&#39;ordine delle righe all&#39;interno della partizione della finestra.

#### schema_of_json

`schema_of_json(json[, options])`: Restituisce lo schema nel formato DDL della stringa JSON.

Esempio:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Dal: 2.4.0

#### frasi

`sentences(str[, lang, country])`: Divide `str` in un array di parole.

Esempio:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### sequence

`sequence(start, stop, step)`: Genera un array di elementi dall&#39;inizio all&#39;arresto (incluso), incrementando passo per passo. Il tipo degli elementi restituiti è uguale al tipo di espressioni di argomento.

I tipi supportati sono: byte, short, integer, long, date, timestamp.

Le espressioni `start` e `stop` devono essere risolte allo stesso tipo. Se `start` e `stop` le espressioni vengono risolte al tipo &quot;data&quot; o &quot;timestamp&quot;, l&#39; `step` espressione deve essere risolta al tipo &quot;intervallo&quot;; in caso contrario, viene risolto nello stesso tipo delle espressioni `start` e `stop` .

Argomenti:
- `start`: Un&#39;espressione. L&#39;inizio dell&#39;intervallo.
- `stop`: Un&#39;espressione. La fine dell&#39;intervallo (incluso).
- `step`: Un&#39;espressione facoltativa. Il passo dell&#39;intervallo. Per impostazione predefinita `step` è 1 se `start` è minore o uguale a `stop`, altrimenti -1. Per le sequenze temporali è rispettivamente 1 giorno e -1 giorno. Se `start` è maggiore di `stop`, il `step` valore deve essere negativo e viceversa.

Esempi:

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Dal: 2.4.0

#### shift

`shiftleft(base, expr)`: Spostamento a sinistra bit a bit.

Esempio:

```
> SELECT shiftleft(2, 1);
 4
```

#### shift

`shiftright(base, expr)`: Spostamento a destra bit a bit (con segno).

Esempio:

```
> SELECT shiftright(4, 1);
 2
```

#### shiftrightunsigned

`shiftrightunsigned(base, expr)`: Spostamento a destra bit a bit senza segno.

Esempio:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`: Restituisce la dimensione di un array o di una mappa. La funzione restituisce -1 se il relativo input è nullo e `spark.sql.legacy.sizeOfNull` è impostato su true. Se `spark.sql.legacy.sizeOfNull` è impostata su false, la funzione restituisce null per l&#39;input nullo. Per impostazione predefinita, il `spark.sql.legacy.sizeOfNull` parametro è impostato su true.

Esempi:

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### space

`space(n)`: Restituisce una stringa costituita da `n` spazi.

Esempio:

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`: Divide `str` intorno alle occorrenze corrispondenti `regex`.

Esempio:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Restituisce la sottostringa da `str` prima `count` delle occorrenze del delimitatore `delim`. Se `count` è positivo, viene restituito tutto a sinistra del delimitatore finale (conteggio da sinistra). Se `count` è negativo, viene restituito tutto a destra del delimitatore finale (contando da destra). La funzione `substring_index` esegue una corrispondenza con distinzione tra maiuscole e minuscole durante la ricerca `delim`.

Esempio:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Restituisce un array di stringhe di valori all&#39;interno dei nodi del codice xml che corrispondono all&#39;espressione XPath.

Esempio:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`: Restituisce un valore doppio, il valore zero se non viene trovata alcuna corrispondenza, NaN se viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Restituisce un valore float, il valore zero se non viene trovata alcuna corrispondenza o NaN se viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Restituisce un valore intero, oppure il valore zero se non viene trovata alcuna corrispondenza, oppure viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Restituisce un valore intero lungo, oppure il valore zero se non viene trovata alcuna corrispondenza, oppure viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Restituisce un valore doppio, il valore zero se non viene trovata alcuna corrispondenza, NaN se viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Restituisce un valore intero breve, oppure il valore zero se non viene trovata alcuna corrispondenza, oppure viene trovata una corrispondenza ma il valore non è numerico.

Esempio:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Restituisce il contenuto del testo del primo nodo xml che corrisponde all&#39;espressione XPath.

Esempio:

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Informazioni correnti {#current-information}

#### current_database

`current_database()`: Restituisce il database corrente.

Esempio:

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: Restituisce la data corrente all&#39;inizio della valutazione della query.

Dal: 1,5,0

#### current_timestamp

`current_timestamp()`: Restituisce la marca temporale corrente all&#39;inizio della valutazione della query.

Dal: 1,5,0

#### now

`now()`: Restituisce la marca temporale corrente all&#39;inizio della valutazione della query.

Dal: 1,5,0

### Funzioni di ordine superiore {#higher-order}

#### transform

`transform(array, lambdaExpression): array`

Trasformare gli elementi in un array utilizzando la funzione.

Se sono presenti due argomenti per la funzione lambda, il secondo argomento indica l&#39;indice dell&#39;elemento.

Esempio:

```
> SELECT transform(array(1, 2, 3), x -> x + 1);
  [2,3,4]
> SELECT transform(array(1, 2, 3), (x, i) -> x + i);
  [1,3,5]
```


#### exists

`exists(array, lambdaExpression returning Boolean): Boolean`

Verificare se un predicato contiene uno o più elementi nell&#39;array.

Esempio:

```
> SELECT exists(array(1, 2, 3), x -> x % 2 == 0);
  true
```

#### filter

`filter(array, lambdaExpression returning Boolean): array`

Filtrare l&#39;array di input utilizzando il predicato specificato.

Esempio:

```
> SELECT filter(array(1, 2, 3), x -> x % 2 == 1);
 [1,3]
```


#### aggregato

`aggregate(array, <initial accumulator value>, lambdaExpression to accumulate the value): array`

Applicate un operatore binario a uno stato iniziale e a tutti gli elementi dell&#39;array, e riducetelo a un singolo stato. Lo stato finale viene convertito nel risultato finale applicando una funzione di fine.

Esempio:

```
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x);
  6
> SELECT aggregate(array(1, 2, 3), 0, (acc, x) -> acc + x, acc -> acc * 10);
  60
```
