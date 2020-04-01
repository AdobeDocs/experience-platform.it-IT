---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eliminare un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 85b497d87fcfb54f390302036ce24c98c6dba6ff

---


# Eliminare un oggetto

È possibile eliminare un oggetto Catalog inserendo il relativo ID nel percorso di una richiesta DELETE.

>[!WARNING] Presta particolare attenzione quando elimini gli oggetti, in quanto questo non può essere annullato e può produrre modifiche rivoluzionarie altrove in Experience Platform.

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto Catalog da eliminare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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
