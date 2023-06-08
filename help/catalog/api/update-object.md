---
keywords: Experience Platform;home;argomenti popolari;catalogo;api;aggiornare un oggetto
solution: Experience Platform
title: Aggiornare un oggetto catalogo
description: Per aggiornare parte di un oggetto Catalog, devi includere il relativo ID nel percorso di una richiesta PATCH. In questo documento viene descritto l’utilizzo dei campi e della notazione Patch JSON per l’esecuzione di operazioni PATCH sugli oggetti Catalog.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---

# Aggiornare un oggetto Catalog

È possibile aggiornare parte di un [!DNL Catalog] includendo il relativo ID nel percorso di una richiesta PATCH. Questo documento descrive i due metodi per eseguire operazioni PATCH sugli oggetti Catalog:

* Utilizzo dei campi
* Utilizzo della notazione patch JSON

>[!NOTE]
>
>Le operazioni PATCH su un oggetto non possono modificare i relativi campi espandibili, che rappresentano oggetti intercorrelati. Le modifiche agli oggetti correlati devono essere effettuate direttamente.

## Aggiorna utilizzando i campi

La chiamata di esempio seguente illustra come aggiornare un oggetto utilizzando campi e valori.

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da aggiornare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna il `name` e `description` campi di un set di dati ai valori forniti nel payload. I campi oggetto che non devono essere aggiornati possono essere esclusi dal payload.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. L’esecuzione di una richiesta di GET per questo set di dati ora mostra che solo il `name` e `description` sono stati aggiornati, mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aggiorna utilizzando la notazione patch JSON

La chiamata di esempio seguente illustra come aggiornare un oggetto utilizzando Patch JSON, come descritto in [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da aggiornare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna il `name` e `description` campi di un set di dati ai valori forniti in ciascun oggetto Patch JSON. Quando utilizzi la patch JSON, devi anche impostare l’intestazione Content-Type su `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID dell’oggetto aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. Quando si esegue una richiesta di GET per questo oggetto, ora viene mostrato che solo `name` e `description` sono stati aggiornati, mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
