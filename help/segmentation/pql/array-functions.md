---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni di array, elenco e set
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 5%

---


# Funzioni di array, elenco e set

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con array, elenchi e stringhe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## In

La `in` funzione viene utilizzata per determinare se un elemento è un membro di una matrice o di un elenco.

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

La `notIn` funzione viene utilizzata per determinare se un elemento non è un membro di una matrice o di un elenco.

>[!NOTE]
>
>La `notIn` funzione assicura *inoltre* che nessuno dei due valori sia uguale a null. Pertanto, i risultati non sono una negazione esatta della `in` funzione.

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

La `intersects` funzione viene utilizzata per determinare se due array o elenchi hanno almeno un membro comune.

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

La `intersection` funzione viene utilizzata per determinare i membri comuni di due array o elenchi.

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

La `subsetOf` funzione viene utilizzata per determinare se una matrice specifica (array A) è un sottoinsieme di un altro array (array B). In altre parole, tutti gli elementi dell&#39;array A sono elementi dell&#39;array B.

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

La `supersetOf` funzione viene utilizzata per determinare se un array specifico (array A) è un superset di un altro array (array B). In altre parole, l&#39;array A contiene tutti gli elementi dell&#39;array B.

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

La `includes` funzione viene utilizzata per determinare se un array o un elenco contiene un elemento specificato.

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

La `distinct` funzione viene utilizzata per rimuovere i valori duplicati da un array o da un elenco.

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

La `groupBy` funzione viene utilizzata per suddividere i valori di un array o di un elenco in un gruppo in base al valore dell&#39;espressione.

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

La `filter` funzione viene utilizzata per filtrare un array o un elenco basato su un&#39;espressione.

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

La `map` funzione viene utilizzata per creare un nuovo array applicando un&#39;espressione a ogni elemento di un dato array.

**Formato**

```sql
array.map(expression)
```

**Esempio**

La seguente query PQL crea una nuova matrice di numeri e quadrati il valore dei numeri originali.

```sql
numbers.map(square)
```

## Primo `n` array

La `topN` funzione viene utilizzata per restituire i primi `N` elementi di un array, se ordinati in ordine crescente in base alla specifica espressione numerica.

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

## Ultimo `n` nell&#39;array

La `bottomN` funzione viene utilizzata per restituire gli ultimi `N` elementi di un array, se ordinati in ordine crescente in base alla specifica espressione numerica.

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

La `head` funzione viene utilizzata per restituire il primo elemento nell&#39;array o nell&#39;elenco.

**Formato**

```sql
{ARRAY}.head()
```

**Esempio**

La seguente query PQL restituisce il primo dei primi cinque ordini con il prezzo più alto. Ulteriori informazioni sulla `topN` funzione sono reperibili nella [prima `n` sezione della matrice](#first-n-in-array) .

```sql
orders.topN(price, 5).head()
```

## Passaggi successivi

Dopo aver appreso le funzioni di array, elenco e set, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
