---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sostituire un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# Sostituire un oggetto

Potete sovrascrivere il contenuto di un [!DNL Catalog] oggetto utilizzando una richiesta di PUT in cui l&#39;intera risorsa viene sostituita con il payload della richiesta.

>[!NOTE]
>
>Se è necessario aggiornare solo alcuni campi specifici all&#39;interno di un [!DNL Catalog] oggetto, l&#39;utilizzo di una richiesta PATCH potrebbe essere più efficiente.

**Formato API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da sostituire. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico da aggiornare. |

**Richiesta**

La seguente richiesta sovrascrive un dataset con i valori forniti nel payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Risposta**

Una risposta corretta restituisce un array contenente l&#39;ID dell&#39;oggetto sovrascritto. Questo ID deve corrispondere a quello inviato nella richiesta PUT. L&#39;esecuzione di una richiesta di GET per questo oggetto ora mostra che i relativi dettagli sono stati sostituiti con quelli forniti nel payload della richiesta di PUT precedente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
