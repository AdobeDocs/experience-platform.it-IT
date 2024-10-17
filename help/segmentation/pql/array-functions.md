---
solution: Experience Platform
title: Funzioni Array, List e Set PQL
description: Profile Query Language (PQL) offre funzioni per semplificare l’interazione con array, elenchi e stringhe.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 4%

---

# Funzioni array, list e set

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con array, elenchi e stringhe. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## In entrata

La funzione `in` viene utilizzata per determinare se un elemento è membro di un array o di un elenco come booleano.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno cade in marzo, giugno o settembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Non in

La funzione `notIn` viene utilizzata per determinare se un elemento non è un membro di un array o di un elenco come booleano.

>[!NOTE]
>
>La funzione `notIn` *also* assicura che nessuno dei due valori sia uguale a null. Pertanto, i risultati non sono una negazione esatta della funzione `in`.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Esempio**

La seguente query PQL definisce gli utenti con compleanni che non sono in marzo, giugno o settembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Interseca

La funzione `intersects` viene utilizzata per determinare se due matrici o elenchi hanno almeno un membro comune come booleano.

**Formato**

```sql
{ARRAY}.intersects({ARRAY})
```

**Esempio**

La seguente query PQL definisce gli utenti i cui colori preferiti includono almeno uno rosso, blu o verde.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Intersezione 

La funzione `intersection` viene utilizzata per determinare i membri comuni di due array o elenchi come elenco.

**Formato**

```sql
{ARRAY}.intersection({ARRAY})
```

**Esempio**

La seguente query PQL definisce se la persona 1 e la persona 2 hanno entrambi i colori preferiti rosso, blu e verde.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Sottoinsieme di

La funzione `subsetOf` viene utilizzata per determinare se un array specifico (array A) è un sottoinsieme di un altro array (array B). In altre parole, che tutti gli elementi nell’array A sono elementi dell’array B come booleano.

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

La funzione `supersetOf` viene utilizzata per determinare se un array specifico (array A) è un superset di un altro array (array B). In altre parole, l’array A contiene tutti gli elementi dell’array B come booleano.

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

La funzione `includes` viene utilizzata per determinare se un array o un elenco contiene un dato elemento come booleano.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Esempio**

La seguente query PQL definisce gli utenti il cui colore preferito include il rosso.

```sql
person.favoriteColors.includes("red")
```

## Diverso

La funzione `distinct` viene utilizzata per rimuovere i valori duplicati da un array o da un elenco come array.

**Formato**

```sql
{ARRAY}.distinct()
```

**Esempio**

La query PQL seguente specifica gli utenti che hanno effettuato ordini in più store.

```sql
person.orders.storeId.distinct().count() > 1
```

## Raggruppa per

La funzione `groupBy` viene utilizzata per suddividere i valori di un array o di un elenco in un gruppo in base al valore dell&#39;espressione come mappa da valori univoci dell&#39;espressione di raggruppamento ad array che sono partizioni del valore dell&#39;espressione di matrice.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da raggruppare. |
| `{EXPRESSION}` | Espressione che esegue il mapping di ogni elemento nell&#39;array o nell&#39;elenco restituito. |

**Esempio**

La query PQL seguente raggruppa tutti gli ordini in base ai quali è stato effettuato l&#39;ordine.

```sql
xEvent[type="order"].groupBy(storeId)
```

## Filtro

La funzione `filter` viene utilizzata per filtrare un array o un elenco in base a un&#39;espressione come array o elenco, a seconda dell&#39;input.

**Formato**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da filtrare. |
| `{EXPRESSION}` | Espressione in base alla quale filtrare. |

**Esempio**

La seguente query PQL definisce tutte le persone di età pari o superiore a 21 anni.

```sql
person.filter(age >= 21)
```

## Mappa

La funzione `map` viene utilizzata per creare un nuovo array applicando un&#39;espressione a ogni elemento in un determinato array come array.

**Formato**

```sql
array.map(expression)
```

**Esempio**

La query PQL seguente crea una nuova matrice di numeri e quadra il valore dei numeri originali.

```sql
numbers.map(square)
```

## Primi `n` nell&#39;array {#first-n}

La funzione `topN` viene utilizzata per restituire i primi `N` elementi in un array, se ordinati in ordine crescente in base alla data espressione numerica come array.

**Formato**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da ordinare. |
| `{VALUE}` | Proprietà in cui ordinare l&#39;array o l&#39;elenco. |
| `{AMOUNT}` | Il numero di elementi da restituire. |

**Esempio**

La query PQL seguente restituisce i primi cinque ordini con il prezzo più alto.

```sql
orders.topN(price, 5)
```

## Ultimi `n` nell&#39;array

La funzione `bottomN` viene utilizzata per restituire gli ultimi `N` elementi in un array, se ordinati in ordine crescente in base alla data espressione numerica come array.

**Formato**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argomento | Descrizione |
| --------- | ----------- | 
| `{ARRAY}` | Matrice o elenco da ordinare. |
| `{VALUE}` | Proprietà in cui ordinare l&#39;array o l&#39;elenco. |
| `{AMOUNT}` | Il numero di elementi da restituire. |

**Esempio**

La query PQL seguente restituisce i primi cinque ordini con il prezzo più basso.

```sql
orders.bottomN(price, 5)
```

## Primo elemento

La funzione `head` viene utilizzata per restituire il primo elemento dell&#39;array o dell&#39;elenco come oggetto.

**Formato**

```sql
{ARRAY}.head()
```

**Esempio**

La query PQL seguente restituisce il primo dei primi cinque ordini con il prezzo più alto. Ulteriori informazioni sulla funzione `topN` sono disponibili nella sezione [first `n` in array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Passaggi successivi

Dopo aver appreso le funzioni array, elenco e impostazione, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
