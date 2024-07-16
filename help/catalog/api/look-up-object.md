---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti;api
solution: Experience Platform
title: Cercare un oggetto catalogo
description: Se conosci l’identificatore univoco di un oggetto Catalog specifico, puoi eseguire una richiesta di GET per visualizzarne i dettagli.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Cercare un oggetto Catalog

Se si conosce l&#39;identificatore univoco di un oggetto [!DNL Catalog] specifico, è possibile eseguire una richiesta di GET per visualizzare i dettagli dell&#39;oggetto.

>[!NOTE]
>
>Quando si visualizzano oggetti specifici, è comunque consigliabile [filtrare in base alle proprietà](filter-data.md) e restituire solo le proprietà desiderate.

**Formato API**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera recuperare. |

**Richiesta**

La richiesta seguente recupera un set di dati in base al relativo ID, restituendo le proprietà `name`, `description`, `tags` e `files`.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce il set di dati specificato con solo il `properties` richiesto nel corpo.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Le proprietà i cui valori sono preceduti da `@` rappresentano oggetti intercorrelati. Per informazioni su come visualizzare i dettagli di questi oggetti, vedere la sezione dell&#39;appendice relativa alla visualizzazione di [oggetti intercorrelati](appendix.md#view-interrelated-objects).
