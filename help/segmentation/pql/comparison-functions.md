---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;servizio di segmentazione;pql;PQL;Profile Query Language;comparison functions;comparison functions;
solution: Experience Platform
title: Funzioni di confronto PQL
description: Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi, restituendo di conseguenza "true" o "false".
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# Funzioni di confronto

Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi, restituendo `true` o `false` di conseguenza. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È uguale a

Il `=` (uguale a) controlla se un valore o un&#39;espressione è uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} = {VALUE}
```

**Esempio**

La query PQL seguente verifica se il paese dell’indirizzo principale si trova in Canada.

```sql
homeAddress.countryISO = "CA"
```

## Non uguale

Il `!=` (diverso da) controlla se un valore o un’espressione è **non** uguale a un altro valore o espressione.

**Formato**

```sql
{EXPRESSION} != {VALUE}
```

**Esempio**

La query PQL seguente verifica se il paese dell’indirizzo dell’abitazione non si trova in Canada.

```sql
homeAddress.countryISO != "CA"
```

## Maggiore di

Il `>` (maggiore di) per verificare se il primo valore è maggiore del secondo valore.

**Formato**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno non cade in gennaio o febbraio.

```sql
person.birthMonth > 2
```

## Maggiore o uguale a

Il `>=` (maggiore o uguale a) per verificare se il primo valore è maggiore o uguale al secondo valore.

**Formato**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Esempio**

La seguente query PQL definisce le persone il cui compleanno non cade in gennaio o febbraio.

```sql
person.birthMonth >= 3
```

## Minore di

Il `<` La funzione di confronto (minore di) viene utilizzata per verificare se il primo valore è minore del secondo valore.

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

Il `<=` (minore o uguale a) per verificare se il primo valore è minore o uguale al secondo valore.

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

Ora che hai imparato le funzioni di confronto, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
