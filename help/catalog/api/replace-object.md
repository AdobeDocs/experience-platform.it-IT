---
keywords: Experience Platform;home;argomenti popolari;catalogo;api;sostituire un oggetto
solution: Experience Platform
title: Sostituire un oggetto catalogo
description: Puoi sovrascrivere il contenuto di un oggetto Catalog utilizzando una richiesta PUT, in cui l’intera risorsa viene sostituita con il payload della richiesta.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 3%

---

# Sostituire un oggetto Catalog

È possibile sovrascrivere il contenuto di un oggetto [!DNL Catalog] utilizzando una richiesta PUT, in cui l&#39;intera risorsa viene sostituita con il payload della richiesta.

>[!NOTE]
>
>Se è necessario aggiornare solo alcuni campi specifici all&#39;interno di un oggetto [!DNL Catalog], l&#39;utilizzo di una richiesta PATCH potrebbe risultare più efficiente.

**Formato API**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da sostituire. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente sovrascrive un set di dati con i valori forniti nel payload.

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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array contenente l’ID dell’oggetto sovrascritto. Questo ID deve corrispondere a quello inviato nella richiesta PUT. L’esecuzione di una richiesta GET per questo oggetto ora mostra che i relativi dettagli sono stati sostituiti con quelli forniti nel payload della richiesta PUT precedente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
