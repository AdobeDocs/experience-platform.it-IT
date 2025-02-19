---
keywords: Experience Platform;home;argomenti popolari;catalogo;api;aggiornare un oggetto
solution: Experience Platform
title: Aggiornare un oggetto catalogo
description: Per aggiornare parte di un oggetto Catalog, devi includere il relativo ID nel percorso di una richiesta PATCH. Questo documento illustra l’utilizzo dei campi e della notazione Patch JSON per l’esecuzione di operazioni PATCH sugli oggetti Catalogo.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Aggiornare un oggetto Catalog

È possibile aggiornare parte di un oggetto [!DNL Catalog] includendo il relativo ID nel percorso di una richiesta PATCH. Questo documento descrive i due metodi per eseguire operazioni PATCH sugli oggetti Catalog:

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
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da aggiornare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna i campi `name` e `description` di un set di dati ai valori forniti nel payload. I campi oggetto che non devono essere aggiornati possono essere esclusi dal payload.

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

In caso di esito positivo, la risposta restituisce un array contenente l’ID del set di dati aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. L&#39;esecuzione di una richiesta GET per questo set di dati ora mostra che solo `name` e `description` sono stati aggiornati, mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aggiorna utilizzando la notazione patch JSON {#patch-notation}

La chiamata di esempio seguente illustra come aggiornare un oggetto utilizzando la patch JSON, come descritto in [RFC-6902](https://tools.ietf.org/html/rfc6902).

Per ulteriori informazioni sulla sintassi delle patch JSON, consulta la [guida sui concetti fondamentali dell&#39;API](../../landing/api-fundamentals.md#json-patch).

**Formato API**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da aggiornare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente aggiorna i campi `name` e `description` di un set di dati ai valori forniti in ciascun oggetto Patch JSON. Quando si utilizza la patch JSON, è necessario impostare anche l’intestazione Content-Type su `application/json-patch+json`.

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

In caso di esito positivo, la risposta restituisce un array contenente l’ID dell’oggetto aggiornato. Questo ID deve corrispondere a quello inviato nella richiesta PATCH. L&#39;esecuzione di una richiesta GET per questo oggetto ora mostra che solo `name` e `description` sono stati aggiornati mentre tutti gli altri valori rimangono invariati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aggiorna utilizzando la notazione di PATCH v2 {#patch-v2-notation}

L&#39;endpoint `/v2/dataSets/{DATASET_ID}` offre un modo più flessibile per aggiornare attributi di set di dati complessi o con nidificazione approfondita.

In genere, quando si aggiorna un campo nidificato in modo profondo (ad esempio `a.b.c.d`), ogni livello nel percorso deve già esistere. Se manca un livello, è necessario crearne manualmente uno prima di impostare il valore finale. Questo richiede spesso operazioni multiple, che aggiungono complessità e aumentano la probabilità di errori.

L&#39;endpoint `/v2/dataSets/{DATASET_ID}` crea automaticamente tutti i livelli mancanti nel percorso. Anziché controllare e aggiungere manualmente `b` e `c` prima di impostare `d`, l&#39;operazione PATCH `v2` esegue questa operazione automaticamente.

Quando si invia una richiesta PATCH all&#39;endpoint `/v2/dataSets/{DATASET_ID}`, è sufficiente inviare la struttura finale e il sistema inserisce le parti mancanti prima di applicare l&#39;aggiornamento.

>[!NOTE]
>
>`If-Match` e `If-None-Match` intestazioni sono facoltative per l&#39;endpoint `/v2/dataSets/{id}`. Le richieste di PATCH a questo endpoint uniscono in modo dinamico gli aggiornamenti, consentendo modifiche senza recuperare la versione più recente del set di dati. Anche se questo riduce il rischio di perdita di dati da aggiornamenti simultanei, è possibile utilizzare `If-Match` con l&#39;ultimo `etag` per garantire che le modifiche si applichino solo a una versione specifica. In alternativa, `If-None-Match` impedisce gli aggiornamenti se il set di dati non è stato modificato dall&#39;ultima versione nota.

**Formato API**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{DATASET_ID}` | Identificatore del set di dati da aggiornare. |

**Richiesta**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID del set di dati aggiornato, che deve corrispondere all’ID inviato nella richiesta PATCH. L&#39;esecuzione di una richiesta GET per questo oggetto ora indica che l&#39;oggetto `extensions.adobe_lakeHouse.rowExpiration` è stato creato senza richiedere passaggi di creazione manuali precedenti.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Un esempio di set di dati prima e dopo l’aggiornamento

L&#39;esempio di JSON seguente illustra la struttura del set di dati **prima** della richiesta PATCH, in cui l&#39;oggetto `extensions.adobe_lakeHouse.rowExpiration` non è presente nel set di dati.

+++Seleziona per visualizzare l’esempio

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

Il seguente JSON mostra la struttura del set di dati **dopo** la richiesta PATCH. L&#39;aggiornamento crea automaticamente l&#39;oggetto `extensions.adobe_lakeHouse.rowExpiration` mancante senza precedenti passaggi di creazione manuale. In questo esempio viene illustrato come la richiesta PATCH `/v2/` elimina la necessità di più operazioni, rendendo gli aggiornamenti più semplici ed efficienti.


+++Seleziona per visualizzare l’esempio

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
