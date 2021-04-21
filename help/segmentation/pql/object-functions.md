---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;pql;PQL;Lingua query profilo;funzioni oggetto;oggetto;
solution: Experience Platform
title: Funzioni dell'oggetto PQL
topic-legacy: developer guide
description: Il Profile Query Language (PQL) offre funzioni che semplificano l’interazione con gli oggetti.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# Funzioni dell&#39;oggetto

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l’interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## È nullo

La funzione `isNull` determina se un riferimento a un oggetto non esiste.

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

La funzione `isNotNull` determina se esiste un riferimento a un oggetto.

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

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle all&#39;interno delle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, consulta la [Panoramica di Profile Query Language](./overview.md).
