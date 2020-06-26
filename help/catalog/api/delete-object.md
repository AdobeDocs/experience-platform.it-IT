---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eliminare un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 327be13cbaaa40e4d0409cbb49a051b7067759bf
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# Eliminare un oggetto

Potete eliminare un oggetto Catalog inserendo il relativo ID nel percorso di una richiesta di DELETE.

>[!WARNING] Prestate particolare attenzione quando eliminate degli oggetti, in quanto questo non può essere annullato e potrebbe causare modifiche di interruzione in altre aree di  Experience Platform.

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>L&#39; `DELETE /batches/{ID}` endpoint è stato dichiarato obsoleto. Per eliminare un batch, è necessario utilizzare l&#39;API [di](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)inserimento batch.

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da eliminare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente elimina un dataset il cui ID è specificato nel percorso della richiesta.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e una matrice contenente l&#39;ID del set di dati eliminato. Questo ID deve corrispondere a quello inviato nella richiesta DELETE. L&#39;esecuzione di una richiesta GET sull&#39;oggetto eliminato restituisce lo stato HTTP 404 (non trovato), confermando che il set di dati è stato eliminato correttamente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Se nessun oggetto Catalog corrisponde all’ID fornito nella richiesta, potreste comunque ricevere un codice di stato HTTP 200, ma l’array di risposte sarà vuoto.
