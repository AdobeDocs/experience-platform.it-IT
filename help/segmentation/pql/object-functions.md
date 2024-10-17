---
solution: Experience Platform
title: Funzioni oggetto di PQL
description: Profile Query Language (PQL) offre funzioni per semplificare l’interazione con gli oggetti.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 8%

---

# Funzioni oggetto

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l&#39;interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni di PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È Null

La funzione `isNull` determina se un riferimento a un oggetto non esiste come booleano.

**Formato**

```sql
{OBJECT}.isNull()
```

**Esempio**

La query PQL seguente verifica se l’indirizzo dell’abitazione della persona non esiste.

```sql
person.homeAddress.isNull()
```

## Non è Null

La funzione `isNotNull` determina se un riferimento a un oggetto esiste come booleano.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Esempio**

La query PQL seguente verifica se l’indirizzo dell’abitazione della persona esiste.

```sql
person.homeAddress.isNotNull()
```

## Passaggi successivi

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni su altre funzioni di PQL, leggere la [panoramica di Profile Query Language](./overview.md).
