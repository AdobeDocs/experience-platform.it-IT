---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni booleane
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 5%

---


# Funzioni booleane

Le funzioni booleane vengono utilizzate per eseguire logica booleana su elementi diversi in [!DNL Profile Query Language] (PQL).  Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## And

La `and` funzione viene utilizzata per creare una combinazione logica.

**Formato**

```sql
{QUERY} and {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con il paese di origine come Canada e l&#39;anno di nascita del 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oppure

La `or` funzione viene utilizzata per creare una disgiunzione logica.

**Formato**

```sql
{QUERY} or {QUERY}
```

**Esempio**

La seguente query PQL restituirà tutte le persone con il paese di origine come Canada o anno di nascita del 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Not

La funzione `not` (o `!`) viene utilizzata per creare una negazione logica.

**Formato**

```sql
not ({QUERY})
!({QUERY})
```

**Esempio**

La seguente query PQL restituirà tutte le persone che non hanno il proprio paese di origine come Canada.

```sql
not (homeAddress.countryISO = "CA")
```

## If

La `if` funzione viene utilizzata per risolvere un&#39;espressione a seconda che una condizione specificata sia vera.

**Formato**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argomento | Descrizione |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | L&#39;espressione booleana in fase di test. |
| `{TRUE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è true. |
| `{FALSE_EXPRESSION}` | L&#39;espressione il cui valore verrà utilizzato se `{TEST_EXPRESSION}` è false. |

**Esempio**

La seguente query PQL imposta il valore come `1` se il paese di origine è il Canada e `2` se il paese di origine non è il Canada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Passaggi successivi

Dopo aver appreso le funzioni booleane, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
