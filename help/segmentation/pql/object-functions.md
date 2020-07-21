---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funzioni dell'oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# Funzioni dell&#39;oggetto

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella panoramica [Lingua query](./overview.md)profilo.

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