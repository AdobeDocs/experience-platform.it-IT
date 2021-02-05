---
keywords: ' Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti;api'
solution: Experience Platform
title: Cercare un oggetto catalogo
topic: developer guide
description: 'Se si conosce l''identificatore univoco di un oggetto Catalog specifico, è possibile eseguire una richiesta di GET per visualizzare i dettagli dell''oggetto. '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# Cercare un oggetto Catalog

Se si conosce l&#39;identificatore univoco di un oggetto specifico [!DNL Catalog], è possibile eseguire una richiesta di GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Durante la visualizzazione di oggetti specifici, è comunque consigliabile filtrare in base alle proprietà [e restituire solo le proprietà interessate.](filter-data.md)

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera recuperare. |

**Richiesta**

La richiesta seguente recupera un dataset dal relativo ID, restituendo le proprietà `name`, `description`, `state`, `tags` e `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il set di dati specificato con solo la `properties` richiesta nel corpo.

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
>Le proprietà i cui valori hanno il prefisso `@` rappresentano oggetti correlati. Per informazioni su come visualizzare i dettagli di questi oggetti, vedere la sezione dell&#39;appendice relativa alla [visualizzazione di oggetti correlati](appendix.md#view-interrelated-objects).
