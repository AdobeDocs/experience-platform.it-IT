---
title: Impaginazione delle risposte nell’API di Reactor
description: Scopri come impaginare i risultati quando inserisci le risorse nell’API di Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Impaginazione delle risposte nell’API di Reactor

Le risposte restituite dall’API di Reactor sono impaginate. La dimensione predefinita della pagina è di 25 elementi. I dettagli sull’impaginazione sono riportati nella sezione `meta.pagination `dell’oggetto di risposta API:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

È possibile ottenere una pagina specifica e modificare le dimensioni di una pagina includendo un parametro di query `page` nel percorso della richiesta.

## Recupera una pagina specifica

Per ottenere una pagina specifica:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Modificare le dimensioni della pagina

Per modificare le dimensioni della pagina:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

È possibile combinare diverse opzioni:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
