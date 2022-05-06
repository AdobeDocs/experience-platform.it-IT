---
keywords: Experience Platform;home;argomenti comuni;filtro;filtrare;filtrare dati;filtrare dati
solution: Experience Platform
title: Elenco oggetti catalogo
topic-legacy: developer guide
description: È possibile recuperare un elenco di tutti gli oggetti disponibili di un tipo specifico tramite una singola chiamata API, in cui la best practice prevede l’inclusione di filtri che limitano la dimensione della risposta.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 2%

---

# Elenco oggetti del catalogo

È possibile recuperare un elenco di tutti gli oggetti disponibili di un tipo specifico tramite una singola chiamata API, in cui la best practice prevede l’inclusione di filtri che limitano la dimensione della risposta.

**Formato API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da elencare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Parametro di query utilizzato per filtrare i risultati restituiti nella risposta. Più parametri sono separati da una e commerciale (`&`). Consulta la guida su [filtraggio dei dati del catalogo](filter-data.md) per ulteriori informazioni. |

**Richiesta**

La richiesta di esempio seguente recupera un elenco di set di dati con un `limit` filtrare la risposta in base a cinque risultati, e `properties` filtro che limita le proprietà visualizzate per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di [!DNL Catalog] oggetti sotto forma di coppie chiave-valore, filtrati dai parametri di query forniti nella richiesta. Per ogni coppia chiave-valore, la chiave rappresenta un identificatore univoco per [!DNL Catalog] oggetto in questione, che può quindi essere utilizzato in un&#39;altra chiamata a [visualizza l&#39;oggetto specifico](look-up-object.md) per ulteriori dettagli.

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
