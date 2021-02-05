---
keywords: ' Experience Platform;home;argomenti popolari;segmentazione;segmentazione;Segmentation Service;pql;PQL;Profile Query Language;object function;object;'
solution: Experience Platform
title: Funzioni dell'oggetto PQL
topic: developer guide
description: Il linguaggio PQL (Profile Query Language) offre funzioni che semplificano l'interazione con gli oggetti.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---


# Funzioni dell&#39;oggetto

[!DNL Profile Query Language] (PQL) offre funzioni che semplificano l&#39;interazione con gli oggetti. Ulteriori informazioni sulle altre funzioni PQL sono disponibili nella [[!DNL Profile Query Language] panoramica](./overview.md).

## Null

La funzione `isNull` determina se un riferimento a un oggetto non esiste.

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

La funzione `isNotNull` determina se esiste un riferimento a un oggetto.

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

Dopo aver appreso le funzioni oggetto, è possibile utilizzarle nelle query PQL. Per ulteriori informazioni sulle altre funzioni PQL, leggere la [Panoramica del linguaggio di query profilo](./overview.md).