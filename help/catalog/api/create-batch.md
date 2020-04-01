---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un dataset
topic: developer guide
translation-type: tm+mt
source-git-commit: a25ca22fb8ec9eb95f74e4fd76a7f18e87343085

---


# Creare un batch

Affinché un dataset possa acquisire i dati, deve essere associato a un batch. Utilizzando il `id` valore di un set di dati esistente, potete creare un batch effettuando una richiesta POST all’ `/batches` endpoint nell’API Catalog.

**Formato API**

```HTTP
POST /batches
```

**Richiesta**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `datasetId` | Il set `id` di dati a cui sarà associato il batch. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto risposta contenente i dettagli del batch appena creato, inclusa `id`una stringa generata dal sistema di sola lettura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
