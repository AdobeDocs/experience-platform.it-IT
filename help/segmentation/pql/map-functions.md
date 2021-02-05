---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segmentation Service;pql;PQL;Profile Query Language;map function;map;'
solution: Experience Platform
title: Funzioni Mappa PQL
topic: developer guide
description: Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l'interazione con le mappe.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---


# Mappa, funzioni

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con le mappe. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

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

## Tasti

La funzione `keys` viene utilizzata per recuperare tutti i tasti di una determinata mappa.

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

Ora che hai imparato le funzioni delle mappe, puoi usarle nelle tue query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).
