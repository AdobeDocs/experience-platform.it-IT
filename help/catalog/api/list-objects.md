---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elenca gli oggetti
topic: developer guide
translation-type: tm+mt
source-git-commit: 71c73a3899ccdd1c024a811b36c411915a3b14be

---


# Elenca gli oggetti

È possibile recuperare un elenco di tutti gli oggetti disponibili di un tipo specifico tramite una singola chiamata API, con la procedura consigliata di includere filtri che limitano le dimensioni della risposta.

**Formato API**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da elencare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Parametro di query utilizzato per filtrare i risultati restituiti nella risposta. Più parametri sono separati da e-mail (`&`). Per ulteriori informazioni, consultate la guida sul [filtro dei dati](filter-data.md) del catalogo. |

**Richiesta**

La richiesta di esempio seguente recupera un elenco di set di dati, con un `limit` filtro che riduce la risposta a cinque risultati, e un `properties` filtro che limita le proprietà visualizzate per ogni set di dati.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un elenco di oggetti Catalog sotto forma di coppie chiave-valore, filtrati dai parametri di query forniti nella richiesta. Per ogni coppia chiave-valore, la chiave rappresenta un identificatore univoco per l&#39;oggetto Catalog in questione, che può essere utilizzato in un&#39;altra chiamata per [visualizzare l&#39;oggetto](look-up-object.md) specifico per ulteriori dettagli.

>[!NOTE] Se un oggetto restituito non contiene una o più delle proprietà richieste indicate dalla `properties` query, la risposta restituisce solo le proprietà richieste che non include, come mostrato in &quot;Sample Dataset 3&quot; e &quot;Sample Dataset 4&quot; di seguito.

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
