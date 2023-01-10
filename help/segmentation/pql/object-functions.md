---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni oggetto;oggetto;
solution: Experience Platform
title: Funzioni dell'oggetto PQL
description: Il Profile Query Language (PQL) offre funzioni che semplificano l’interazione con gli oggetti.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# Funzioni oggetto

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l’interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella sezione [[!DNL Profile Query Language] panoramica](./overview.md).

## È nullo

La `isNull` determina se un riferimento a un oggetto non esiste.

**Formato**

```sql
{OBJECT}.isNull()
```

**Esempio**

La seguente query PQL controlla se l&#39;indirizzo di origine della persona non esiste.

```sql
person.homeAddress.isNull()
```

## Non è Null

La `isNotNull` determina se esiste un riferimento a un oggetto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Esempio**

La seguente query PQL controlla se l&#39;indirizzo di casa della persona esiste.

```sql
person.homeAddress.isNotNull()
```

## Passaggi successivi

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere il [Panoramica della lingua della query del profilo](./overview.md).
