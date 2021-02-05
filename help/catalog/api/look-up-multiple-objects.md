---
keywords: ' Experience Platform;home;argomenti popolari;catalogo;ricerca di più oggetti;api'
solution: Experience Platform
title: Ricerca di più oggetti catalogo
topic: developer guide
description: Se si desidera visualizzare diversi oggetti specifici, anziché effettuare una richiesta per oggetto, Catalog fornisce una semplice scelta rapida per richiedere più oggetti dello stesso tipo. Potete utilizzare una singola richiesta di GET per restituire più oggetti specifici includendo un elenco di ID separati da virgola.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---


# Cercare più oggetti catalogo

Se si desidera visualizzare diversi oggetti specifici, invece di effettuare una richiesta per oggetto, [!DNL Catalog] fornisce una semplice scelta rapida per richiedere più oggetti dello stesso tipo. Potete utilizzare una singola richiesta di GET per restituire più oggetti specifici includendo un elenco di ID separati da virgola.

>[!NOTE]
>
>Anche quando si richiedono specifici oggetti [!DNL Catalog], è comunque consigliabile utilizzare il parametro di query `properties` per restituire solo le proprietà necessarie.

**Formato API**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parametro | Descrizione |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da recuperare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Identificatore di uno degli oggetti specifici che si desidera recuperare. |

**Richiesta**

La richiesta seguente include un elenco separato da virgole di ID di set di dati e un elenco separato da virgole di proprietà da restituire per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco dei set di dati specificati, contenente solo le proprietà richieste (`name`, `description` e `files`) per ciascuno di essi.

>[!NOTE]
>
>Se un oggetto restituito non contiene una o più delle proprietà richieste indicate dalla query `properties`, la risposta restituisce solo le proprietà richieste che non include, come mostrato in ***`Sample Dataset 3`*** e ***`Sample Dataset 4`*** di seguito.

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
