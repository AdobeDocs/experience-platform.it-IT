---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;pql;PQL;Profile Query Language;funzioni di array;array;'
solution: Experience Platform
title: Funzioni Array, List e Set PQL
topic: developer guide
description: Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l'interazione con array, elenchi e stringhe.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---


# Funzioni di array, elenco e set

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con array, elenchi e stringhe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## In

La funzione `in` viene utilizzata per determinare se un elemento è un membro di una matrice o di un elenco.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone con compleanni a marzo, giugno o settembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

La funzione `notIn` viene utilizzata per determinare se un elemento non è un membro di una matrice o di un elenco.

>[!NOTE]
>
>La funzione `notIn` *anche* assicura che nessuno dei due valori sia uguale a null. Pertanto, i risultati non sono una negazione esatta della funzione `in`.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone con compleanni che non sono in marzo, giugno o settembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Interseca

La funzione `intersects` viene utilizzata per determinare se due array o elenchi hanno almeno un membro comune.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Esempio**

La seguente query PQL definisce le persone i cui colori preferiti includono almeno uno di rosso, blu o verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersection

La funzione `intersection` viene utilizzata per determinare i membri comuni di due array o elenchi.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Esempio**

La seguente query PQL definisce se la persona 1 e la persona 2 hanno entrambi i colori preferiti di rosso, blu e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Sottoinsieme di

La funzione `subsetOf` viene utilizzata per determinare se un array specifico (array A) è un sottoinsieme di un altro array (array B). In altre parole, tutti gli elementi dell&#39;array A sono elementi dell&#39;array B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Esempio**

La seguente query PQL definisce le persone che hanno visitato tutte le loro città preferite.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset di

La funzione `supersetOf` viene utilizzata per determinare se un array specifico (array A) è un superset di un altro array (array B). In altre parole, l&#39;array A contiene tutti gli elementi dell&#39;array B.

**Formato**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Esempio**

La seguente query PQL definisce le persone che hanno mangiato sushi e pizza almeno una volta.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Include

La funzione `includes` viene utilizzata per determinare se un array o un elenco contiene un elemento specificato.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Esempio**

La seguente query PQL definisce le persone il cui colore preferito include il rosso.

```sql
person.favoriteColors.includes("red")
```

## Distinto

La funzione `distinct` viene utilizzata per rimuovere i valori duplicati da un array o da un elenco.

**Formato**

```sql
{ARRAY}.distinct()
```

**Esempio**

La seguente query PQL specifica le persone che hanno effettuato ordini in più store.

```sql
person.orders.storeId.distinct().count() > 1
```

## Raggruppa per

La funzione `groupBy` viene utilizzata per suddividere i valori di un array o di un elenco in un gruppo in base al valore dell&#39;espressione.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | L&#39;array o l&#39;elenco da raggruppare. |
| `{EXPRESSION}` | Espressione che mappa ogni elemento nell&#39;array o nell&#39;elenco restituito. |

**Esempio**

La seguente query PQL raggruppa tutti gli ordini in base ai quali viene memorizzato l&#39;ordine.

```sql
orders.groupBy(storeId)
```

## Filtro

La funzione `filter` viene utilizzata per filtrare un array o un elenco basato su un&#39;espressione.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | L&#39;array o l&#39;elenco da filtrare. |
| `{EXPRESSION}` | Espressione da cui filtrare. |

**Esempio**

La seguente query PQL definisce tutte le persone con almeno 21 anni di età.

```sql
person.filter(age >= 21)
```

## Mappa

La funzione `map` viene utilizzata per creare una nuova matrice applicando un&#39;espressione a ogni elemento di una determinata matrice.

**Formato**

```sql
array.map(expression)
```

**Esempio**

La seguente query PQL crea una nuova matrice di numeri e quadrati il valore dei numeri originali.

```sql
numbers.map(square)
```

## Primo `n` nell&#39;array {#first-n}

La funzione `topN` viene utilizzata per restituire i primi `N` elementi di un array, se ordinati in ordine crescente in base alla data espressione numerica.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | L&#39;array o l&#39;elenco da ordinare. |
| `{VALUE}` | La proprietà in cui ordinare l&#39;array o l&#39;elenco. |
| `{AMOUNT}` | Numero di elementi da restituire. |

**Esempio**

La seguente query PQL restituisce i primi cinque ordini con il prezzo più alto.

```sql
orders.topN(price, 5)
```

## Ultima `n` nella matrice

La funzione `bottomN` viene utilizzata per restituire gli ultimi `N` elementi di un array, se ordinati in ordine crescente in base alla data espressione numerica.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- | 
| `{ARRAY}` | L&#39;array o l&#39;elenco da ordinare. |
| `{VALUE}` | La proprietà in cui ordinare l&#39;array o l&#39;elenco. |
| `{AMOUNT}` | Numero di elementi da restituire. |

**Esempio**

La seguente query PQL restituisce i primi cinque ordini con il prezzo più basso.

```sql
orders.bottomN(price, 5)
```

## Primo elemento

La funzione `head` viene utilizzata per restituire il primo elemento dell&#39;array o dell&#39;elenco.

**Formato**

```sql
{ARRAY}.head()
```

**Esempio**

La seguente query PQL restituisce il primo dei primi cinque ordini con il prezzo più alto. Ulteriori informazioni sulla funzione `topN` sono disponibili nella sezione [prima `n` della matrice](#first-n).

```sql
orders.topN(price, 5).head()
```

## Passaggi successivi

Dopo aver appreso le funzioni di array, elenco e set, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).
