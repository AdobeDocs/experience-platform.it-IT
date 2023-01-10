---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni array;array;
solution: Experience Platform
title: Funzioni Array, List e Set PQL
description: Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l’interazione con array, elenchi e stringhe.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# Funzioni Array, list e set

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l’interazione con array, elenchi e stringhe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## In

La `in` viene utilizzata per determinare se un elemento è membro di una matrice o di un elenco.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone con i compleanni a marzo, giugno o settembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Non in

La `notIn` viene utilizzata per determinare se un elemento non è membro di una matrice o di un elenco.

>[!NOTE]
>
>La `notIn` Funzione *anche* assicura che nessuno dei due valori sia uguale a null. Pertanto, i risultati non sono una negazione esatta del `in` funzione .

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone con compleanni che non si trovano a marzo, giugno o settembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersecazioni

La `intersects` viene utilizzata per determinare se due array o elenchi hanno almeno un membro comune.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Esempio**

La seguente query PQL definisce le persone i cui colori preferiti includono almeno uno di rosso, blu o verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersezione

La `intersection` viene utilizzata per determinare i membri comuni di due array o elenchi.

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

La `subsetOf` viene utilizzata per determinare se un array specifico (array A) è un sottoinsieme di un altro array (array B). In altre parole, tutti gli elementi dell&#39;array A sono elementi dell&#39;array B.

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

La `supersetOf` viene utilizzata per determinare se un array specifico (array A) è un superset di un altro array (array B). In altre parole, l&#39;array A contiene tutti gli elementi dell&#39;array B.

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

La `includes` viene utilizzata per determinare se una matrice o un elenco contiene un elemento specificato.

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

La `distinct` viene utilizzata per rimuovere i valori duplicati da una matrice o da un elenco.

**Formato**

```sql
{ARRAY}.distinct()
```

**Esempio**

La seguente query PQL specifica le persone che hanno effettuato ordini in più di un archivio.

```sql
person.orders.storeId.distinct().count() > 1
```

## Raggruppa per

La `groupBy` viene utilizzata per suddividere i valori di una matrice o di un elenco in un gruppo in base al valore dell&#39;espressione.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da raggruppare. |
| `{EXPRESSION}` | Espressione che mappa ogni elemento della matrice o dell&#39;elenco restituito. |

**Esempio**

La seguente query PQL raggruppa tutti gli ordini in base ai quali è stato effettuato l’ordine di archiviazione.

```sql
orders.groupBy(storeId)
```

## Filtro

La `filter` viene utilizzata per filtrare un array o un elenco in base a un&#39;espressione.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da filtrare. |
| `{EXPRESSION}` | Espressione da cui filtrare. |

**Esempio**

La seguente query PQL definisce tutte le persone che hanno 21 anni o più.

```sql
person.filter(age >= 21)
```

## Mappa

La `map` viene utilizzata per creare un nuovo array applicando un&#39;espressione a ogni elemento di un array specifico.

**Formato**

```sql
array.map(expression)
```

**Esempio**

La seguente query PQL crea una nuova matrice di numeri e quadra il valore dei numeri originali.

```sql
numbers.map(square)
```

## Primo `n` in matrice {#first-n}

La `topN` viene utilizzata per restituire il primo `N` elementi in una matrice, se ordinati in ordine crescente in base all&#39;espressione numerica specificata.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da ordinare. |
| `{VALUE}` | Proprietà in cui ordinare la matrice o l&#39;elenco. |
| `{AMOUNT}` | Numero di elementi da restituire. |

**Esempio**

La seguente query PQL restituisce i primi cinque ordini con il prezzo più alto.

```sql
orders.topN(price, 5)
```

## Ultimo `n` in matrice

La `bottomN` viene utilizzata per restituire l&#39;ultima `N` elementi in una matrice, se ordinati in ordine crescente in base all&#39;espressione numerica specificata.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- | 
| `{ARRAY}` | Matrice o elenco da ordinare. |
| `{VALUE}` | Proprietà in cui ordinare la matrice o l&#39;elenco. |
| `{AMOUNT}` | Numero di elementi da restituire. |

**Esempio**

La seguente query PQL restituisce i primi cinque ordini con il prezzo più basso.

```sql
orders.bottomN(price, 5)
```

## Primo elemento

La `head` viene utilizzata per restituire il primo elemento dell&#39;array o dell&#39;elenco.

**Formato**

```sql
{ARRAY}.head()
```

**Esempio**

La seguente query PQL restituisce il primo dei primi cinque ordini con il prezzo più alto. Ulteriori informazioni sulle `topN` si trova nella [first `n` in matrice](#first-n) sezione .

```sql
orders.topN(price, 5).head()
```

## Passaggi successivi

Dopo aver appreso le informazioni sull&#39;array, l&#39;elenco e l&#39;impostazione delle funzioni, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
