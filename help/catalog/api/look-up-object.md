---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti;api
solution: Experience Platform
title: Ricerca di un oggetto catalogo
topic-legacy: developer guide
description: Se si conosce l'identificatore univoco di un oggetto Catalog specifico, è possibile eseguire una richiesta GET per visualizzare i dettagli dell'oggetto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# Cercare un oggetto Catalogo

Se si conosce l&#39;identificatore univoco di un oggetto specifico [!DNL Catalog], è possibile eseguire una richiesta GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Durante la visualizzazione di oggetti specifici, è comunque consigliabile [filtrare in base alle proprietà](filter-data.md) e restituire solo le proprietà di interesse.

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

La richiesta seguente recupera un set di dati dal relativo ID e restituisce le proprietà `name`, `description`, `state`, `tags` e `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il set di dati specificato con solo il `properties` richiesto nel corpo.

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
>Le proprietà i cui valori sono preceduti da `@` rappresentano oggetti correlati. Per istruzioni su come visualizzare i dettagli di questi oggetti, vedere la sezione dell&#39;appendice relativa alla [visualizzazione di oggetti correlati](appendix.md#view-interrelated-objects).
