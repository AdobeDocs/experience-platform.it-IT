---
keywords: ' Experience Platform;home;argomenti più comuni;dataset;Dataset;creare un dataset;creare un dataset;abilitare il dataset'
solution: Experience Platform
title: Creare un dataset
topic: developer guide
description: In questo documento viene illustrato come creare un oggetto dataset in Catalog.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%

---


# Creare un dataset

Per creare un dataset utilizzando l&#39;API [!DNL Catalog], è necessario conoscere il valore `$id` dello schema [!DNL Experience Data Model] (XDM) su cui verrà basato il dataset. Una volta ottenuto l&#39;ID dello schema, è possibile creare un dataset effettuando una richiesta di POST all&#39;endpoint `/datasets` nell&#39;API [!DNL Catalog].

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
| `schemaRef.id` | Il valore URI `$id` per lo schema XDM su cui si baserà il dataset. |

>[!NOTE]
>
>In questo esempio viene utilizzato il formato di file [Apache Parquet](https://parquet.apache.org/documentation/latest/) per la relativa proprietà `containerFormat`. Un esempio che utilizza il formato di file JSON si trova nella [guida per gli sviluppatori di assimilazione batch](../../ingestion/batch-ingestion/api-overview.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto response costituito da una matrice contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L&#39;ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
