---
title: Impaginazione delle risposte nell’API di Reactor
description: Scopri come impaginare i risultati quando generi un elenco di risorse nell’API di Reactor.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 86%

---

# Impaginazione delle risposte nell’API di Reactor

Le risposte restituite dall’API di Reactor sono impaginate. La dimensione predefinita della pagina prevede 25 elementi. I dettagli sull&#39;impaginazione sono riportati nella sezione `meta.pagination` dell&#39;oggetto di risposta API:

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

Per ottenere una pagina specifica e modificare le dimensioni di una pagina, includi un parametro di query `page` nel percorso della richiesta.

## Recuperare una pagina specifica

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
