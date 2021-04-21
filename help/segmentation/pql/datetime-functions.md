---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni data e ora;funzioni datetime;datetime;data;ora;
solution: Experience Platform
title: Funzioni di data e ora PQL
topic-legacy: developer guide
description: Le funzioni di data e ora vengono utilizzate per eseguire operazioni di data e ora sui valori all’interno di Profile Query Language (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 4%

---

# Funzioni di data e ora

Le funzioni di data e ora vengono utilizzate per eseguire operazioni di data e ora sui valori all&#39;interno di [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Mese corrente

La funzione `currentMonth` restituisce il mese corrente sotto forma di numero intero.

**Formato**

```sql
currentMonth()
```

**Esempio**

La seguente query PQL controlla se il mese di nascita della persona è il mese corrente.

```sql
person.birthMonth = currentMonth()
```

## Ottieni mese

La funzione `getMonth` restituisce il mese, come numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getMonth()
```

**Esempio**

La seguente query PQL controlla se il mese di nascita della persona è in giugno.

```sql
person.birthdate.getMonth() = 6
```

## Anno corrente

La funzione `currentYear` restituisce l&#39;anno corrente come numero intero.

**Formato**

```sql
currentYear()
```

**Esempio**

La seguente query PQL verifica se il prodotto è stato venduto nell’anno corrente.

```sql
product.saleYear = currentYear()
```

## Ottieni anno

La funzione `getYear` restituisce l&#39;anno, come numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Esempio**

La seguente interrogazione PQL controlla se l&#39;anno di nascita della persona cade nel 1991, 1992, 1993, 1994 o 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Giorno corrente del mese

La funzione `currentDayOfMonth` restituisce il giorno corrente del mese come numero intero.

**Formato**

```sql
currentDayOfMonth()
```

**Esempio**

La seguente query PQL controlla se il giorno di nascita della persona corrisponde al giorno corrente del mese.

```sql
person.birthDay = currentDayOfMonth()
```

## Ottieni giorno del mese

La funzione `getDayOfMonth` restituisce il giorno, come numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Esempio**

La seguente query PQL controlla se l’articolo è stato venduto entro i primi 15 giorni del mese.

```sql
product.sale.getDayOfMonth() <= 15
```

## Si verifica

La funzione `occurs` confronta la funzione di marca temporale specificata con un periodo di tempo fisso.

**Formato**

La funzione `occurs` può essere scritta utilizzando uno dei seguenti formati:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{COMPARISON}` | Operatore di confronto. Può essere uno dei seguenti operatori: `>`, `>=`, `<`, `<=`, `=`, `!=`. Ulteriori informazioni sulle funzioni di confronto sono disponibili nel documento [funzioni di confronto](./comparison-functions.md). |
| `{INTEGER}` | Un numero intero non negativo. |
| `{TIME_UNIT}` | Unità di tempo. Può essere una delle seguenti parole: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Una preposizione che descrive quando confrontare la data in. Può essere una delle seguenti parole: `before`, `after`, `from`. |
| `{TIME}` | Può essere un valore letterale di marca temporale (`today`, `now`, `yesterday`, `tomorrow`), un&#39;unità di tempo relativa (una di `this`, `last` o `next` seguita da un&#39;unità di tempo) o un attributo di marca temporale. |

>[!NOTE]
>
>L&#39;utilizzo della parola `on` è facoltativo. È disponibile per migliorare la leggibilità di alcune combinazioni, ad esempio `timestamp occurs on date(2019,12,31)`.

**Esempio**

La seguente query PQL controlla se l&#39;articolo è stato venduto la settimana scorsa.

```sql
product.saleDate occurs last week
```

La seguente query PQL verifica se un articolo è stato venduto tra l’8 gennaio 2015 e il 1° luglio 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Subito

`now` è una parola riservata che rappresenta la marca temporale dell’esecuzione PQL.

**Esempio**

La seguente query PQL controlla se un articolo è stato venduto esattamente tre ore prima.

```sql
product.saleDate occurs = 3 hours before now
```

## Oggi

`today` è una parola riservata che rappresenta la marca temporale dell’inizio del giorno dell’esecuzione PQL.

**Esempio**

La seguente query PQL controlla se il compleanno di una persona è stato tre giorni fa.

```sql
person.birthday occurs = 3 days before today
```

## Passaggi successivi

Dopo aver appreso le funzioni di data e ora, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
