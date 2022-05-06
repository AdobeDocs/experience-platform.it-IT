---
keywords: Experience Platform;home;argomenti popolari;catalogo;api;sostituire un oggetto
solution: Experience Platform
title: Sostituire un oggetto catalogo
topic-legacy: developer guide
description: Puoi sovrascrivere il contenuto di un oggetto Catalog utilizzando una richiesta PUT, dove l’intera risorsa viene sostituita con il payload della richiesta.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 3%

---

# Sostituire un oggetto Catalog

Puoi sovrascrivere il contenuto di un [!DNL Catalog] oggetto utilizzando una richiesta PUT, in cui l’intera risorsa viene sostituita con il payload della richiesta.

>[!NOTE]
>
>Se devi aggiornare solo alcuni campi specifici all’interno di un [!DNL Catalog] l&#39;utilizzo di una richiesta PATCH può essere più efficiente.

**Formato API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da sostituire. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera aggiornare. |

**Richiesta**

La seguente richiesta sovrascrive un set di dati con i valori forniti nel payload.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Una risposta corretta restituisce un array contenente l&#39;ID dell&#39;oggetto sovrascritto. Questo ID deve corrispondere a quello inviato nella richiesta di PUT. L&#39;esecuzione di una richiesta GET per questo oggetto ora mostra che i relativi dettagli sono stati sostituiti con quelli forniti nel payload della richiesta PUT precedente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
