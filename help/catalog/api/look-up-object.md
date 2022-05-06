---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti;api
solution: Experience Platform
title: Ricerca di un oggetto catalogo
topic-legacy: developer guide
description: Se si conosce l'identificatore univoco di un oggetto Catalog specifico, è possibile eseguire una richiesta GET per visualizzare i dettagli dell'oggetto.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Cercare un oggetto Catalogo

Se conosci l’identificatore univoco per uno specifico [!DNL Catalog] è possibile eseguire una richiesta GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Quando si visualizzano oggetti specifici, è comunque consigliabile [filtrare in base alle proprietà](filter-data.md) e restituire solo le proprietà che ti interessano.

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

La seguente richiesta recupera un set di dati dal relativo ID e restituisce il relativo `name`, `description`, `state`, `tags`e `files` proprietà.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce il set di dati specificato con solo il set di dati richiesto `properties` nel corpo.

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
>Proprietà i cui valori hanno il prefisso `@` rappresentano oggetti correlati. Vedi la sezione dell&#39;appendice su [visualizzazione di oggetti correlati](appendix.md#view-interrelated-objects) per informazioni su come visualizzare i dettagli di questi oggetti.
