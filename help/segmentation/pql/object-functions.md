---
solution: Experience Platform
title: Funzioni oggetto PQL
description: PQL (Profile Query Language) offre funzioni per semplificare l’interazione con gli oggetti.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 6%

---

# Funzioni oggetto

[!DNL Profile Query Language] (PQL) offre funzioni per semplificare l&#39;interazione con gli oggetti. Ulteriori informazioni su altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È nullo

Il `isNull` determina se un riferimento a un oggetto non esiste.

**Formato**

```sql
{OBJECT}.isNull()
```

**Esempio**

La query PQL seguente verifica se l’indirizzo dell’abitazione della persona non esiste.

```sql
person.homeAddress.isNull()
```

## Non è nullo

Il `isNotNull` determina se esiste un riferimento a un oggetto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Esempio**

La query PQL seguente verifica se l&#39;indirizzo dell&#39;abitazione della persona esiste.

```sql
person.homeAddress.isNotNull()
```

## Passaggi successivi

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni su altre funzioni PQL, leggere [Panoramica sulla lingua delle query di profilo](./overview.md).
