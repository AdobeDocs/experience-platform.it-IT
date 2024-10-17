---
solution: Experience Platform
title: Funzioni di PQL Map
description: Profile Query Language (PQL) offre funzioni per semplificare l’interazione con le mappe.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# Funzioni di mappatura

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l&#39;interazione con le mappe. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Ottieni

La funzione `get` viene utilizzata per recuperare il valore di una mappa per una determinata chiave come oggetto.

**Formato**

```sql
{MAP}.get({STRING})
```

**Esempio**

La seguente query PQL ottiene il valore della mappa identità per la chiave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Chiavi

La funzione `keys` viene utilizzata per recuperare tutte le chiavi per una determinata mappa come array o elenco.

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

La funzione `values` viene utilizzata per recuperare tutti i valori di una determinata mappa come array o elenco.

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

Ora che hai imparato le funzioni mappa, puoi utilizzarle all’interno delle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
