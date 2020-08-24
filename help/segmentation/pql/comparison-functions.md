---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni di confronto
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 10%

---


# Funzioni di confronto

Le funzioni di confronto sono utilizzate per confrontare espressioni e valori diversi, restituendo `true` o `false` di conseguenza. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È uguale a

La funzione `=` (equals) controlla se un valore o un&#39;espressione è uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Esempio**

La seguente query PQL verifica se il paese dell&#39;indirizzo di origine è in Canada.

```sql
homeAddress.countryISO = "CA"
```

## Non uguale

La funzione `!=` (non uguale) controlla se un valore o un&#39;espressione **non** è uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Esempio**

La seguente query PQL verifica se il paese dell&#39;indirizzo di origine non è in Canada.

```sql
homeAddress.countryISO != "CA"
```

## Maggiore di

La funzione `>` (maggiore di) viene utilizzata per verificare se il primo valore è maggiore del secondo valore.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone i cui compleanni non rientrano in gennaio o febbraio.

```sql
person.birthMonth > 2
```

## Maggiore o uguale a

La funzione `>=` (maggiore o uguale a) viene utilizzata per verificare se il primo valore è maggiore o uguale al secondo valore.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone i cui compleanni non rientrano in gennaio o febbraio.

```sql
person.birthMonth >= 3
```

## Minore di

La funzione di confronto `<` (minore di) viene utilizzata per verificare se il primo valore è minore del secondo.

**Formato**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno è in gennaio.

```sql
person.birthMonth < 2
```

## Minore o uguale a

La funzione di confronto `<=` (minore o uguale a) viene utilizzata per verificare se il primo valore è minore o uguale al secondo valore.

**Formato**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno è in gennaio o febbraio.

```sql
person.birthMonth <= 2
```

## Passaggi successivi

Ora che hai imparato le funzioni di confronto, puoi usarle nelle tue query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
