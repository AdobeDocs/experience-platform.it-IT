---
title: Ordinamento delle risposte nell’API del reattore
description: Scopri come filtrare i risultati quando inserisci le risorse nell’API di Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Ordinamento delle risposte nell’API di Reactor

L’elenco degli endpoint nell’API di Reactor ti consente di ordinare le risorse restituite in base agli attributi specificati. Puoi configurare l’ordinamento della risposta fornendo un parametro `sort` nel percorso della richiesta.

## Ordinamento crescente

Le risorse possono essere ordinate in base a un attributo in ordine crescente specificando
attributo con cui ordinare e prefissarlo con un `+`:

`GET /companies/:company_id/properties?sort=+name`

## Ordinamento decrescente

Le risorse possono essere ordinate in base a un attributo in ordine decrescente specificando
attributo con cui ordinare e prefissarlo con un `-`:

`GET /companies/:company_id/properties?sort=-name`

## Tipi multipli

Per ordinare in base a più valori, fornisci le direttive di ordinamento come separate da virgola
elenco:

`GET /companies/:company_id/properties?sort=+name,-org_id`
