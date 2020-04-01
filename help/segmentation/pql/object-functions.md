---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni dell'oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funzioni dell&#39;oggetto

Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l&#39;interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

## Null

La `isNull` funzione determina se un riferimento a un oggetto non esiste.

**Formato**

```sql
{OBJECT}.isNull()
```

**Esempio**

La seguente query PQL verifica se l&#39;indirizzo della persona non esiste.

```sql
person.homeAddress.isNull()
```

## Non è Null

La `isNotNull` funzione determina se esiste un riferimento a un oggetto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Esempio**

La seguente query PQL verifica se l&#39;indirizzo della persona esiste.

```sql
person.homeAddress.isNotNull()
```

## Passaggi successivi

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consultate la panoramica [Lingua query](./overview.md)profilo.