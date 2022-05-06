---
keywords: Experience Platform;home;argomenti popolari;catalogo;ricerca di più oggetti;api
solution: Experience Platform
title: Ricerca di più oggetti catalogo
topic-legacy: developer guide
description: Se si desidera visualizzare più oggetti specifici, anziché effettuare una richiesta per oggetto, Catalog fornisce una semplice scelta rapida per richiedere più oggetti dello stesso tipo. È possibile utilizzare una singola richiesta di GET per restituire più oggetti specifici includendo un elenco di ID separati da virgole.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Cercare più oggetti Catalogo

Se si desidera visualizzare più oggetti specifici, anziché effettuare una richiesta per oggetto, [!DNL Catalog] fornisce una scelta rapida semplice per richiedere più oggetti dello stesso tipo. È possibile utilizzare una singola richiesta di GET per restituire più oggetti specifici includendo un elenco di ID separati da virgole.

>[!NOTE]
>
>Anche quando si richiedono specifiche [!DNL Catalog] oggetti, è comunque buona prassi `properties` per restituire solo le proprietà necessarie.

**Formato API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Identificatore di uno degli oggetti specifici che si desidera recuperare. |

**Richiesta**

La richiesta seguente include un elenco di ID di set di dati separati da virgole e un elenco di proprietà separate da virgola da restituire per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco dei set di dati specificati, contenente solo le proprietà richieste (`name`, `description`e `files`) per ciascuno di essi.

>[!NOTE]
>
>Se un oggetto restituito non contiene una o più delle proprietà richieste indicate dalla `properties` query, la risposta restituisce solo le proprietà richieste che include, come mostrato in ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** sotto.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
