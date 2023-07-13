---
solution: Experience Platform
title: Funzioni Array, List e Set PQL
description: PQL (Profile Query Language) offre funzioni che semplificano l’interazione con array, elenchi e stringhe.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 5%

---

# Funzioni array, list e set

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l&#39;interazione con array, elenchi e stringhe. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## In

Il `in` viene utilizzata per determinare se un elemento è membro di un array o di un elenco.

**Formato**

```sql
{VALUE} in {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno cade in marzo, giugno o settembre.

```sql
person.birthMonth in [3, 6, 9]
```

## Non in entrata

Il `notIn` viene utilizzata per determinare se un elemento non è un membro di un array o di un elenco.

>[!NOTE]
>
>Il `notIn` funzione *anche* assicura che nessuno dei due valori sia uguale a null. Pertanto, i risultati non sono una negazione esatta del `in` funzione.

**Formato**

```sql
{VALUE} notIn {ARRAY}
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno non è in marzo, giugno o settembre.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

Il `intersects` viene utilizzata per determinare se due array o elenchi hanno almeno un membro comune.

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

Il `intersection` La funzione viene utilizzata per determinare i membri comuni di due array o elenchi.

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

Il `subsetOf` viene utilizzata per determinare se un array specifico (array A) è un sottoinsieme di un altro array (array B). In altre parole, che tutti gli elementi nell&#39;array A sono elementi dell&#39;array B.

**Formato**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Esempio**

La seguente query PQL definisce le persone che hanno visitato tutte le loro città preferite.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Soprainsieme di

Il `supersetOf` viene utilizzata per determinare se un array specifico (array A) è un superset di un altro array (array B). In altre parole, l’array A contiene tutti gli elementi dell’array B.

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

Il `includes` viene utilizzata per determinare se un array o un elenco contiene un dato elemento.

**Formato**

```sql
{ARRAY}.includes({ITEM})
```

**Esempio**

La seguente query PQL definisce gli utenti il cui colore preferito include il rosso.

```sql
person.favoriteColors.includes("red")
```

## Distinct

Il `distinct` viene utilizzata per rimuovere valori duplicati da un array o da un elenco.

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

Il `groupBy` La funzione viene utilizzata per suddividere i valori di un array o di un elenco in un gruppo in base al valore dell’espressione.

**Formato**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{ARRAY}` | Matrice o elenco da raggruppare. |
| `{EXPRESSION}` | Espressione che esegue il mapping di ogni elemento nell&#39;array o nell&#39;elenco restituito. |

**Esempio**

La query PQL seguente raggruppa tutti gli ordini in base ai quali è stato effettuato l&#39;ordine.

```sql
orders.groupBy(storeId)
```

## Filtro

Il `filter` viene utilizzata per filtrare un array o un elenco in base a un’espressione.

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

Il `map` viene utilizzata per creare un nuovo array applicando un’espressione a ogni elemento in un determinato array.

**Formato**

```sql
array.map(expression)
```

**Esempio**

La query PQL seguente crea una nuova matrice di numeri e quadra il valore dei numeri originali.

```sql
numbers.map(square)
```

## Primo `n` nell’array {#first-n}

Il `topN` viene utilizzata per restituire la prima `N` elementi di un array, se ordinati in ordine crescente in base alla data espressione numerica.

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

## Ultimo `n` nell’array

Il `bottomN` viene utilizzata per restituire l&#39;ultimo `N` elementi di un array, se ordinati in ordine crescente in base alla data espressione numerica.

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

Il `head` viene utilizzata per restituire il primo elemento dell’array o dell’elenco.

**Formato**

```sql
{ARRAY}.head()
```

**Esempio**

La query PQL seguente restituisce il primo dei primi cinque ordini con il prezzo più alto. Ulteriori informazioni su `topN` è disponibile nella sezione [primo `n` nell’array](#first-n) sezione.

```sql
orders.topN(price, 5).head()
```

## Passaggi successivi

Dopo aver appreso le funzioni array, list e set, è possibile utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
