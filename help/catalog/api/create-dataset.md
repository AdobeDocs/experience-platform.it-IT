---
keywords: Experience Platform;home;argomenti comuni;set di dati;set di dati;creare un set di dati;abilitare set di dati;home;popular topic;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: Creare un set di dati nell’API
description: Questo documento illustra come creare un oggetto set di dati nell’API Catalog Service.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# Creare un set di dati nell’API

Per creare un set di dati utilizzando l&#39;API [!DNL Catalog], è necessario conoscere il valore `$id` dello schema [!DNL Experience Data Model] (XDM) su cui sarà basato il set di dati. Dopo aver ottenuto l&#39;ID dello schema, puoi creare un set di dati effettuando una richiesta POST all&#39;endpoint `/datasets` nell&#39;API [!DNL Catalog].

>[!NOTE]
>
>In questo documento viene descritto solo come creare un oggetto set di dati in [!DNL Catalog]. Per i passaggi completi su come creare, popolare e monitorare un set di dati, consulta la seguente [esercitazione](../datasets/create.md).

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
| `schemaRef.id` | Il valore URI `$id` per lo schema XDM su cui sarà basato il set di dati. |
| `schemaRef.contentType` | Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul controllo delle versioni dello schema [1} nella guida dell&#39;API XDM.](../../xdm/api/getting-started.md#versioning) |

>[!NOTE]
>
>In questo esempio viene utilizzato il formato di file [Apache Parquet](https://parquet.apache.org/docs/) per la proprietà `containerFormat`. Un esempio che utilizza il formato di file JSON è disponibile nella [guida per gli sviluppatori sull&#39;acquisizione batch](../../ingestion/batch-ingestion/api-overview.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta costituito da un array contenente l’ID del set di dati appena creato in formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema e utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
