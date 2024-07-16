---
solution: Experience Platform
title: Funzioni booleane di PQL
description: Le funzioni booleane vengono utilizzate per eseguire la logica booleana su elementi diversi in Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# Funzioni booleane

Le funzioni booleane vengono utilizzate per eseguire la logica booleana su elementi diversi in [!DNL Profile Query Language] (PQL).  Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## E

La funzione `and` viene utilizzata per creare una congiunzione logica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con paese di origine come Canada e anno di nascita 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oppure

La funzione `or` viene utilizzata per creare una disgiunzione logica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con paese di origine come Canada o anno di nascita 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Non

La funzione `not` (o `!`) viene utilizzata per creare una negazione logica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Esempio**

La seguente query PQL restituirà tutti gli utenti che non hanno il proprio paese di origine come Canada.

```sql
not (homeAddress.countryISO = "CA")
```

## Se

La funzione `if` viene utilizzata per risolvere un&#39;espressione a seconda che una condizione specificata sia vera.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | L’espressione booleana in fase di test. |
| `{TRUE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è true. |
| `{FALSE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è false. |

**Esempio**

La seguente query PQL imposterà il valore come `1` se il paese di origine è il Canada e `2` se il paese di origine non è il Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Passaggi successivi

Ora che hai imparato le funzioni booleane, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
