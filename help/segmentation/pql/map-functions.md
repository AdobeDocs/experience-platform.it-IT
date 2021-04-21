---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni mappa;mappa;
solution: Experience Platform
title: Funzioni Mappa PQL
topic-legacy: developer guide
description: Il Profile Query Language (PQL) offre funzioni per facilitare l’interazione con le mappe.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---

# Mappare le funzioni

[!DNL Profile Query Language] (PQL) offre funzioni che facilitano l’interazione con le mappe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Get

La funzione `get` viene utilizzata per recuperare il valore di una mappa per una determinata chiave.

**Formato**

```sql
{MAP}.get({STRING})
```

**Esempio**

La seguente query PQL ottiene il valore della mappa di identità per la chiave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chiavi

La funzione `keys` viene utilizzata per recuperare tutte le chiavi di una determinata mappa.

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

La funzione `values` viene utilizzata per recuperare tutti i valori di una determinata mappa.

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

Dopo aver appreso le funzioni della mappa, puoi utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
