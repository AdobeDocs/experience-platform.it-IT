---
keywords: Experience Platform;home;argomenti popolari;creare batch;servizio catalogo;api
solution: Experience Platform
title: Creare un batch nell’API
topic-legacy: developer guide
description: Puoi creare un batch effettuando una richiesta POST all’endpoint /batch nell’API del catalogo.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# Creare un batch

Affinché un set di dati possa acquisire dati, deve essere associato a un batch. Utilizzando il valore `id` di un set di dati esistente, puoi creare un batch effettuando una richiesta POST all’endpoint `/batches` nell’ API [!DNL Catalog].

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
| `datasetId` | Il `id` del set di dati a cui sarà associato il batch. |

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta contenente i dettagli del batch appena creato, inclusa la relativa `id`, una stringa generata dal sistema di sola lettura.

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
