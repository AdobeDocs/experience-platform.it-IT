---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Creare un dataset
topic: developer guide
description: In questo documento viene illustrato come creare un oggetto dataset in Catalog.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# Creare un dataset

Per creare un dataset utilizzando l&#39; [!DNL Catalog] API, è necessario conoscere il `$id` valore dello schema [!DNL Experience Data Model] (XDM) su cui si baserà il dataset. Una volta ottenuto l&#39;ID dello schema, potete creare un dataset effettuando una richiesta di POST all&#39; `/datasets` endpoint nell&#39; [!DNL Catalog] API.

>[!NOTE]
>
>Questo documento descrive solo come creare un oggetto dataset in [!DNL Catalog]. Per i passaggi completi su come creare, compilare e monitorare un dataset, fare riferimento alla seguente [esercitazione](../datasets/create.md).

**Formato API**

```HTTP
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un dataset che fa riferimento a uno schema definito in precedenza.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del set di dati da creare. |
| `schemaRef.id` | Il `$id` valore URI per lo schema XDM su cui verrà basato il dataset. |

>[!NOTE]
>
>In questo esempio viene utilizzato il formato di file [parquet](https://parquet.apache.org/documentation/latest/) per la relativa `containerFormat` proprietà. Un esempio che utilizza il formato di file JSON è disponibile nella guida [per gli sviluppatori per l’assimilazione](../../ingestion/batch-ingestion/api-overview.md)batch.

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto response costituito da un array contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L&#39;ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
