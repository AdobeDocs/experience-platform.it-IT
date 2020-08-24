---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mappa, funzioni
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 5%

---


# Mappa, funzioni

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con le mappe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Get

La `get` funzione viene utilizzata per recuperare il valore di una mappa per una determinata chiave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Esempio**

La seguente query PQL ottiene il valore della mappa identità per la chiave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Tasti

La `keys` funzione viene utilizzata per recuperare tutti i tasti di una determinata mappa.

**Formato**

```sql
{MAP}.keys()
```

**Esempio**

La seguente query PQL ottiene tutte le chiavi per la mappa `identityMap`.

```sql
identityMap.keys()
```

## Valori

La `values` funzione viene utilizzata per recuperare tutti i valori di una data mappa.

**Formato**

```sql
{MAP}.values()
```

**Esempio**

La seguente query PQL ottiene tutti i valori per la mappa `identityMap`.

```sql
identityMap.values()
```

## Passaggi successivi

Ora che hai imparato le funzioni delle mappe, puoi usarle nelle tue query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.
