---
keywords: Experience Platform;home;argomenti popolari;filtrare;filtrare;filtrare dati;Filtrare dati
solution: Experience Platform
title: Elenca oggetti catalogo
description: È possibile recuperare un elenco di tutti gli oggetti disponibili di un tipo specifico tramite una singola chiamata API; la best practice prevede l’inclusione di filtri che limitano la dimensione della risposta.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 2%

---

# Elenca oggetti catalogo

È possibile recuperare un elenco di tutti gli oggetti disponibili di un tipo specifico tramite una singola chiamata API; la best practice prevede l’inclusione di filtri che limitano la dimensione della risposta.

**Formato API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da elencare. Gli oggetti validi sono: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | Parametro di query utilizzato per filtrare i risultati restituiti nella risposta. Più parametri separati da e commerciali (`&`). Per ulteriori informazioni, consulta la guida su [filtraggio dei dati del catalogo](filter-data.md). |

**Richiesta**

La richiesta di esempio seguente recupera un elenco di set di dati, con un filtro `limit` che riduce la risposta a cinque risultati e un filtro `properties` che limita le proprietà visualizzate per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un elenco di [!DNL Catalog] oggetti sotto forma di coppie chiave-valore, filtrate dai parametri di query forniti nella richiesta. Per ogni coppia chiave-valore, la chiave rappresenta un identificatore univoco per l&#39;oggetto [!DNL Catalog] in questione, che può quindi essere utilizzato in un&#39;altra chiamata per [visualizzare l&#39;oggetto specifico](look-up-object.md) per ulteriori dettagli.

>[!NOTE]
>
>Se un oggetto restituito non contiene una o più delle proprietà richieste indicate dalla query `properties`, la risposta restituisce solo le proprietà richieste incluse, come illustrato di seguito in ***`Sample Dataset 3`*** e ***`Sample Dataset 4`***.

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
