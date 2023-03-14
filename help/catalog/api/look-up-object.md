---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti;api
solution: Experience Platform
title: Cercare un oggetto catalogo
description: Se conosci l’identificatore univoco di un oggetto Catalog specifico, puoi eseguire una richiesta di GET per visualizzarne i dettagli.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Cercare un oggetto Catalog

Se conosci l’identificatore univoco di un dato [!DNL Catalog] oggetto, è possibile eseguire una richiesta GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Quando si visualizzano oggetti specifici, è comunque consigliabile [filtra per proprietà](filter-data.md) e restituiscono solo le proprietà a cui sei interessato.

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera recuperare. |

**Richiesta**

La richiesta seguente recupera un set di dati in base al suo ID, restituendo il relativo `name`, `description`, `state`, `tags`, e `files` proprietà.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il set di dati specificato con solo il `properties` nel corpo.

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
>Proprietà i cui valori hanno il prefisso `@` rappresentano oggetti intercorrelati. Vedere la sezione dell&#39;appendice relativa a [visualizzazione di oggetti correlati](appendix.md#view-interrelated-objects) per i passaggi su come visualizzare i dettagli di questi oggetti.
