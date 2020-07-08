---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aggiornare un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 3%

---


# Aggiornare un oggetto

Potete aggiornare parte di un oggetto Catalog inserendone l’ID nel percorso di una richiesta PATCH. Questo documento descrive i due metodi per eseguire le operazioni PATCH sugli oggetti Catalog:

* Uso dei campi
* Utilizzo della notazione patch JSON

>[!NOTE]
>
>Le operazioni PATCH su un oggetto non possono modificare i relativi campi espandibili, che rappresentano oggetti correlati.  Le modifiche agli oggetti correlati devono essere apportate direttamente.

## Aggiornamento utilizzando i campi

La seguente chiamata di esempio illustra come aggiornare un oggetto utilizzando campi e valori.

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da aggiornare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico da aggiornare. |

**Richiesta**

La seguente richiesta aggiorna i campi `name` e `description` i campi di un dataset ai valori forniti nel payload. I campi oggetto che non devono essere aggiornati possono essere esclusi dal payload.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. L&#39;esecuzione di una richiesta GET per questo dataset ora mostra che solo il `name` e `description` sono stati aggiornati, mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aggiornamento tramite la notazione patch JSON

La seguente chiamata di esempio illustra come aggiornare un oggetto utilizzando la patch JSON, come descritto in [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da aggiornare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico da aggiornare. |

**Richiesta**

La seguente richiesta aggiorna i campi `name` e `description` di un dataset ai valori forniti in ciascun oggetto Patch JSON. Quando utilizzate la patch JSON, dovete anche impostare l&#39;intestazione Content-Type su `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID dell&#39;oggetto aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. L&#39;esecuzione di una richiesta GET per questo oggetto ora mostra che solo l&#39;oggetto `name` e `description` sono stati aggiornati, mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
