---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni di data e ora
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---


# Funzioni di data e ora

Le funzioni di data e ora sono utilizzate per eseguire operazioni di data e ora sui valori all&#39;interno di [!DNL Profile Query Language] (PQL). Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Mese corrente

La `currentMonth` funzione restituisce il mese corrente come numero intero.

**Formato**

```sql
currentMonth()
```

**Esempio**

La seguente query PQL verifica se il mese di nascita della persona è il mese corrente.

```sql
person.birthMonth = currentMonth()
```

## Ottieni mese

La `getMonth` funzione restituisce il mese, sotto forma di numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getMonth()
```

**Esempio**

La seguente query PQL verifica se il mese di nascita della persona è in giugno.

```sql
person.birthdate.getMonth() = 6
```

## Anno corrente

La `currentYear` funzione restituisce l&#39;anno corrente come numero intero.

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

La `getYear` funzione restituisce l&#39;anno, sotto forma di numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getYear()
```

**Esempio**

La seguente interrogazione PQL verifica se l&#39;anno di nascita della persona cade nel 1991, 1992, 1993, 1994 o 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Giorno corrente del mese

La `currentDayOfMonth` funzione restituisce il giorno corrente del mese come numero intero.

**Formato**

```sql
currentDayOfMonth()
```

**Esempio**

La seguente query PQL verifica se il giorno di nascita della persona corrisponde al giorno corrente del mese.

```sql
person.birthDay = currentDayOfMonth()
```

## Ottieni giorno del mese

La `getDayOfMonth` funzione restituisce il giorno, sotto forma di numero intero, in base a una data marca temporale.

**Formato**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Esempio**

La seguente query PQL verifica se l&#39;articolo è stato venduto entro i primi 15 giorni del mese.

```sql
product.sale.getDayOfMonth() <= 15
```

## Occurs

La `occurs` funzione confronta la funzione timestamp specificata con un periodo di tempo fisso.

**Formato**

La `occurs` funzione può essere scritta utilizzando uno dei seguenti formati:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{COMPARISON}` | Un operatore di confronto. Può essere uno dei seguenti operatori: `>`, `>=`, `<`, `<=`, `=`, `!=`. Ulteriori informazioni sulle funzioni di confronto sono disponibili nel documento [sulle funzioni di](./comparison-functions.md)confronto. |
| `{INTEGER}` | Un numero intero non negativo. |
| `{TIME_UNIT}` | Unità di tempo. Può essere una delle seguenti parole: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries``millennium``millennia`, , . |
| `{DIRECTION}` | Una preposizione che descrive quando confrontare la data con. Può essere una delle seguenti parole: `before`, `after`, `from`. |
| `{TIME}` | Può essere un letterale di marca temporale (`today`, `now`, `yesterday`, `tomorrow`), un&#39;unità di tempo relativa (una di `this`, `last`o `next` seguita da un&#39;unità di tempo) o un attributo di marca temporale. |

>[!NOTE]
>
>L&#39;uso della parola `on` è facoltativo. È disponibile per migliorare la leggibilità di alcune combinazioni, ad esempio `timestamp occurs on date(2019,12,31)`.

**Esempio**

La seguente query PQL verifica se l&#39;articolo è stato venduto la settimana scorsa.

```sql
product.saleDate occurs last week
```

La seguente query PQL verifica se un articolo è stato venduto tra l’8 gennaio 2015 e il 1 luglio 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Adesso

`now` è una parola riservata che rappresenta la marca temporale dell&#39;esecuzione PQL.

**Esempio**

La seguente query PQL verifica se un articolo è stato venduto esattamente tre ore prima.

```sql
product.saleDate occurs = 3 hours before now
```

## Oggi

`today` è una parola riservata che rappresenta la marca temporale dell&#39;inizio del giorno dell&#39;esecuzione PQL.

**Esempio**

La seguente query PQL verifica se il compleanno di una persona è stato tre giorni fa.

```sql
person.birthday occurs = 3 days before today
```

## Passaggi successivi

Ora che hai imparato le funzioni di data e ora, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
