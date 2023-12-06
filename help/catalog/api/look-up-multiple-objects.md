---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca oggetti multipli;api
solution: Experience Platform
title: Cerca più oggetti catalogo
description: Se desideri visualizzare diversi oggetti specifici, anziché effettuare una richiesta per oggetto, Catalog fornisce una semplice scelta rapida per richiedere più oggetti dello stesso tipo. Puoi utilizzare una singola richiesta GET per restituire più oggetti specifici includendo un elenco separato da virgole di ID.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Cercare più oggetti catalogo

Se desideri visualizzare più oggetti specifici, invece di effettuare una richiesta per oggetto, [!DNL Catalog] fornisce una semplice scelta rapida per richiedere più oggetti dello stesso tipo. Puoi utilizzare una singola richiesta GET per restituire più oggetti specifici includendo un elenco separato da virgole di ID.

>[!NOTE]
>
>Anche quando si richiedono [!DNL Catalog] oggetti, è comunque consigliabile `properties` parametro di query per restituire solo le proprietà necessarie.

**Formato API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | Identificatore di uno degli oggetti specifici che si desidera recuperare. |

**Richiesta**

La seguente richiesta include un elenco separato da virgole di ID set di dati e un elenco separato da virgole di proprietà da restituire per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco dei set di dati specificati, contenenti solo le proprietà richieste (`name`, `description`, e `files`) per ciascuno di essi.

>[!NOTE]
>
>Se un oggetto restituito non contiene una o più delle proprietà richieste indicate dal `properties` , la risposta restituisce solo le proprietà richieste che include, come mostrato nella ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** di seguito.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
