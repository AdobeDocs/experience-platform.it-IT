---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;pql;PQL;Profile Query Language;funzioni di aggregazione;aggregazione;'
solution: Experience Platform
title: Funzioni di aggregazione PQL
topic: developer guide
description: 'Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all''interno degli array PQL (Profile Query Language) per creare un singolo valore di riepilogo. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 5%

---


# Funzioni di aggregazione

Le funzioni di aggregazione vengono utilizzate per raggruppare più valori all&#39;interno di array [!DNL Profile Query Language] (PQL) per creare un singolo valore di riepilogo. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Count

La funzione `count` restituisce il numero di elementi all&#39;interno dell&#39;array specificato.

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

La funzione `sum` restituisce la somma di tutti i valori selezionati all&#39;interno dell&#39;array.

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

La funzione `average` restituisce la media aritmetica di tutti i valori selezionati all&#39;interno dell&#39;array.

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

La funzione `min` restituisce il più piccolo di tutti i valori selezionati all&#39;interno dell&#39;array.

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

La funzione `max` restituisce il valore più elevato tra tutti i valori selezionati all&#39;interno dell&#39;array.

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

Dopo aver appreso le funzioni di aggregazione, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).
