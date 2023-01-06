---
keywords: Experience Platform;home;argomenti popolari;eliminare un oggetto;servizio catalogo;api
solution: Experience Platform
title: Eliminare un oggetto nell’API
description: È possibile eliminare un oggetto Catalog fornendo il relativo ID nel percorso di una richiesta DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---

# Eliminare un oggetto nell’API

È possibile eliminare un [!DNL Catalog] fornendo il proprio ID nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Presta particolare attenzione durante l’eliminazione degli oggetti, poiché questa operazione non può essere annullata e può produrre modifiche di interruzione altrove in [!DNL Experience Platform].

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>La `DELETE /batches/{ID}` l&#39;endpoint è stato dichiarato obsoleto. Per eliminare un batch, è necessario utilizzare il [API di acquisizione in batch](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Tipo di [!DNL Catalog] oggetto da eliminare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera aggiornare. |

**Richiesta**

La seguente richiesta elimina un set di dati il cui ID è specificato nel percorso della richiesta.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce lo stato HTTP 200 (OK) e una matrice contenente l&#39;ID del set di dati eliminato. Questo ID deve corrispondere a quello inviato nella richiesta di DELETE. L&#39;esecuzione di una richiesta di GET sull&#39;oggetto eliminato restituisce lo stato HTTP 404 (Non trovato), confermando che il set di dati è stato eliminato correttamente.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se no [!DNL Catalog] Gli oggetti corrispondono all’ID fornito nella richiesta. È comunque possibile che venga ricevuto un codice di stato HTTP 200, ma l’array di risposta sarà vuoto.
