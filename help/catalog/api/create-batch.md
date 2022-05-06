---
keywords: Experience Platform;home;argomenti popolari;creare batch;servizio catalogo;api
solution: Experience Platform
title: Creare un batch nell’API
topic-legacy: developer guide
description: Puoi creare un batch effettuando una richiesta POST all’endpoint /batch nell’API del catalogo.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 5%

---

# Creare un batch

Affinché un set di dati possa acquisire dati, deve essere associato a un batch. Utilizzo della `id` valore di un set di dati esistente, puoi creare un batch effettuando una richiesta di POST al `/batches` punto finale [!DNL Catalog] API.

**Formato API**

```HTTP
POST /batches
```

**Richiesta**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `datasetId` | La `id` del set di dati a cui sarà associato il batch. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del batch appena creato, incluso il relativo `id`, una stringa generata dal sistema di sola lettura.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
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
