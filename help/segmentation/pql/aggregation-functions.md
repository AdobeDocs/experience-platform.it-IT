---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni di aggregazione
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Funzioni di aggregazione

Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all&#39;interno degli array PQL (Profile Query Language) per creare un singolo valore di riepilogo. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## Count

La `count` funzione restituisce il numero di elementi all&#39;interno dell&#39;array specificato.

**Formato**

```sql
{ARRAY}.count()
```

**Esempio**

La seguente query PQL restituisce il numero di ordini nell&#39;array.

```sql
orders.count()
```

## Sum

La `sum` funzione restituisce la somma di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.sum()
```

**Esempio**

La seguente query PQL restituisce la somma di tutti i prezzi degli ordini.

```sql
orders.sum(order.price)
```

## Media

La `average` funzione restituisce la media aritmetica di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.average()
```

**Esempio**

La seguente query PQL restituisce il prezzo medio di tutti gli ordini.

```sql
orders.average(order.price)
```

## Minimo

La `min` funzione restituisce il più piccolo di tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.min()
```

**Esempio**

La seguente query PQL restituisce il prezzo più basso di tutti gli ordini.

```sql
orders.min(order.price)
```

## Massimo

La `max` funzione restituisce il valore più elevato tra tutti i valori selezionati all&#39;interno dell&#39;array.

**Formato**

```sql
{ARRAY}.max()
```

**Esempio**

La seguente query PQL restituisce il prezzo più alto di tutti gli ordini.

```sql
orders.max(order.price)
```

## Passaggi successivi

Dopo aver appreso le funzioni di aggregazione, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
