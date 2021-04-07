---
keywords: Experience Platform;home;argomenti popolari;set di dati;set di dati;creare un set di dati;creare un set di dati;abilitare un set di dati
solution: Experience Platform
title: Creare un set di dati nell’API
topic: guida per sviluppatori
description: Questo documento illustra come creare un oggetto set di dati nell’API del servizio catalogo.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# Creare un set di dati nell’API

Per creare un set di dati utilizzando l’API [!DNL Catalog], è necessario conoscere il valore `$id` dello schema [!DNL Experience Data Model] (XDM) su cui verrà basato il set di dati. Una volta ottenuto l’ID schema, puoi creare un set di dati effettuando una richiesta POST all’endpoint `/datasets` nell’ API [!DNL Catalog] .

>[!NOTE]
>
>Questo documento illustra solo come creare un oggetto set di dati in [!DNL Catalog]. Per i passaggi completi su come creare, compilare e monitorare un set di dati, fai riferimento alla seguente [esercitazione](../datasets/create.md).

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
| `schemaRef.id` | Il valore URI `$id` per lo schema XDM su cui verrà basato il set di dati. |
| `schemaRef.contentType` | Indica il formato e la versione dello schema. Per ulteriori informazioni, consulta la sezione sul [controllo delle versioni dello schema](../../xdm/api/getting-started.md#versioning) nella guida API XDM . |

>[!NOTE]
>
>In questo esempio viene utilizzato il formato di file [Apache Parquet](https://parquet.apache.org/documentation/latest/) per la relativa proprietà `containerFormat`. Un esempio che utilizza il formato di file JSON si trova nella [guida per gli sviluppatori per l’acquisizione batch](../../ingestion/batch-ingestion/api-overview.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 201 (Creato) e un oggetto di risposta costituito da una matrice contenente l&#39;ID del set di dati appena creato nel formato `"@/datasets/{DATASET_ID}"`. L’ID del set di dati è una stringa di sola lettura generata dal sistema che viene utilizzata per fare riferimento al set di dati nelle chiamate API.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
