---
title: Ordinamento delle risposte nell’API di Reactor
description: Scopri come filtrare i risultati quando elenchi le risorse nell’API di Reactor.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---

# Ordinamento delle risposte nell’API di Reactor

Gli endpoint per elenchi nell’API di Reactor consentono di ordinare le risorse restituite in base agli attributi specificati. Per configurare l’ordinamento della risposta, specifica un parametro `sort` nel percorso della richiesta.

## Ordinamento crescente

Le risorse possono essere ordinate in base a un attributo in ordine crescente specificando
l’attributo in questione con il prefisso `+`:

`GET /companies/:company_id/properties?sort=+name`

## Ordinamento decrescente

Le risorse possono essere ordinate in base a un attributo in ordine decrescente specificando
l’attributo in questione con il prefisso `-`:

`GET /companies/:company_id/properties?sort=-name`

## Ordinare in base a più valori

Per ordinare in base a più valori, fornisci le direttive di ordinamento come un elenco separato da virgole:


`GET /companies/:company_id/properties?sort=+name,-org_id`
