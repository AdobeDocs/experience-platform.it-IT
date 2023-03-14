---
keywords: Experience Platform;home;argomenti comuni;set di dati;set di dati;creare un set di dati;abilitare set di dati;home;popular topic;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Creare un set di dati nell’API
description: Questo documento illustra come creare un oggetto set di dati nell’API Catalog Service.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# Creare un set di dati nell’API

Per creare un set di dati utilizzando [!DNL Catalog] API, è necessario conoscere `$id` valore del [!DNL Experience Data Model] Schema (XDM) su cui verrà basato il set di dati. Una volta ottenuto l’ID dello schema, puoi creare un set di dati effettuando una richiesta POST al `/datasets` endpoint nella [!DNL Catalog] API.

>[!NOTE]
>
>Questo documento illustra solo come creare un oggetto set di dati in [!DNL Catalog]. Per i passaggi completi su come creare, popolare e monitorare un set di dati, consulta i seguenti [esercitazione](../datasets/create.md).

**Formato API**

```HTTP
POST /dataSets
```

**Richiesta**

La richiesta seguente crea un set di dati che fa riferimento a uno schema definito in precedenza.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Proprietà | Descrizione |
| --- | --- |
| `name` | Nome del set di dati da creare. |
| `schemaRef.id` | URI `$id` valore per lo schema XDM su cui sarà basato il set di dati. |
| `schemaRef.contentType` | Indica il formato e la versione dello schema. Consulta la sezione su [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) per ulteriori informazioni, consulta la guida dell’API XDM. |

>[!NOTE]
>
>In questo esempio viene utilizzato [Apache Parquet](https://parquet.apache.org/docs/) formato file per i relativi `containerFormat` proprietà. Un esempio che utilizza il formato di file JSON si trova in [guida per gli sviluppatori sull’acquisizione batch](../../ingestion/batch-ingestion/api-overview.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta costituito da un array contenente l’ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
