---
solution: Experience Platform
title: Funzioni di confronto PQL
description: Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi, restituendo di conseguenza "true" o "false".
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# Funzioni di confronto

Le funzioni di confronto vengono utilizzate per confrontare espressioni e valori diversi, restituendo di conseguenza `true` o `false`. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Uguale a

La funzione `=` (è uguale a) controlla se un valore o un&#39;espressione è uguale a un altro valore o espressione.

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

La funzione `!=` (diverso da) controlla se un valore o un&#39;espressione è **diverso** uguale a un altro valore o espressione.

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

La funzione `>` (maggiore di) viene utilizzata per verificare se il primo valore è maggiore del secondo valore.

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

La funzione `>=` (maggiore o uguale a) viene utilizzata per verificare se il primo valore è maggiore o uguale al secondo valore.

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

La funzione di confronto `<` (minore di) viene utilizzata per verificare se il primo valore è minore del secondo valore.

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

Ora che hai imparato le funzioni di confronto, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
