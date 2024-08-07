---
keywords: Experience Platform;home;argomenti popolari;eliminare un oggetto;servizio catalogo;api;home;popular topic;delete an object;catalog service;api
solution: Experience Platform
title: Eliminare un oggetto nell’API
description: Per eliminare un oggetto Catalog, devi fornire il relativo ID nel percorso di una richiesta DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 2%

---

# Eliminare un oggetto nell’API

È possibile eliminare un oggetto [!DNL Catalog] fornendo il relativo ID nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Prestare particolare attenzione durante l&#39;eliminazione degli oggetti, poiché questa operazione non può essere annullata e può causare modifiche che causano interruzioni in altre aree di [!DNL Experience Platform].

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>L&#39;endpoint `DELETE /batches/{ID}` è stato dichiarato obsoleto. Per eliminare un batch, è necessario utilizzare l&#39;[API di acquisizione batch](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di oggetto [!DNL Catalog] da eliminare. Gli oggetti validi sono: <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell’oggetto specifico da aggiornare. |

**Richiesta**

La richiesta seguente elimina un set di dati il cui ID è specificato nel percorso della richiesta.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 (OK) e un array contenente l’ID del set di dati eliminato. Questo ID deve corrispondere a quello inviato nella richiesta DELETE. L’esecuzione di una richiesta GET sull’oggetto eliminato restituisce lo stato HTTP 404 (Non trovato), confermando che il set di dati è stato eliminato correttamente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se nessun oggetto [!DNL Catalog] corrisponde all&#39;ID fornito nella richiesta, è possibile ricevere comunque il codice di stato HTTP 200, ma l&#39;array di risposta sarà vuoto.
