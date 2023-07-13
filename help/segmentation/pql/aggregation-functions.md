---
solution: Experience Platform
title: Funzioni di aggregazione PQL
description: Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all’interno degli array PQL (Profile Query Language) in modo da formare un singolo valore di riepilogo.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 7%

---

# Funzioni di aggregazione

Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all&#39;interno di [!DNL Profile Query Language] (PQL) array per formare un singolo valore di riepilogo. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Conteggio

Il `count` La funzione restituisce il numero di elementi all’interno dell’array specificato.

**Formato**

```sql
{ARRAY}.count()
```

**Esempio**

La query PQL seguente restituisce il numero di ordini nell&#39;array.

```sql
orders.count()
```

## Somma

Il `sum` restituisce la somma di tutti i valori selezionati all’interno dell’array.

**Formato**

```sql
{ARRAY}.sum()
```

**Esempio**

La query PQL seguente restituisce la somma di tutti i prezzi degli ordini.

```sql
orders.sum(order.price)
```

## Medio

Il `average` La funzione restituisce la media aritmetica di tutti i valori selezionati all’interno dell’array.

**Formato**

```sql
{ARRAY}.average()
```

**Esempio**

La query PQL seguente restituisce il prezzo medio di tutti gli ordini.

```sql
orders.average(order.price)
```

## Minimo

Il `min` La funzione restituisce il più piccolo di tutti i valori selezionati all’interno dell’array.

**Formato**

```sql
{ARRAY}.min()
```

**Esempio**

La query PQL seguente restituisce il prezzo più basso di tutti gli ordini.

```sql
orders.min(order.price)
```

## Massimo

Il `max` restituisce il più grande di tutti i valori selezionati all’interno dell’array.

**Formato**

```sql
{ARRAY}.max()
```

**Esempio**

La query PQL seguente restituisce il prezzo più alto di tutti gli ordini.

```sql
orders.max(order.price)
```

## Passaggi successivi

Ora che hai imparato le funzioni di aggregazione, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
