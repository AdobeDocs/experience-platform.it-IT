---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Cercare un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Cercare un oggetto

Se si conosce l&#39;identificatore univoco di un [!DNL Catalog] oggetto specifico, è possibile eseguire una richiesta di GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Durante la visualizzazione di oggetti specifici, è comunque consigliabile [filtrare in base alle proprietà](filter-data.md) e restituire solo le proprietà interessate.

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera recuperare. |

**Richiesta**

La richiesta seguente recupera un dataset dal relativo ID, restituendo le `name`, `description`, `state`, `tags`e `files` le proprietà.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il dataset specificato con solo il set di dati richiesto `properties` nel corpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>Le proprietà i cui valori hanno il prefisso `@` rappresentano oggetti correlati. Per informazioni dettagliate su come visualizzare i dettagli di questi oggetti, vedere la sezione appendice sulla [visualizzazione degli oggetti](appendix.md#view-interrelated-objects) correlati.
