---
keywords: Experience Platform;home;argomenti popolari;eliminare un oggetto;servizio catalogo;api
solution: Experience Platform
title: Eliminare un oggetto nell’API
topic-legacy: developer guide
description: È possibile eliminare un oggetto Catalog fornendo il relativo ID nel percorso di una richiesta DELETE.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# Eliminare un oggetto nell’API

È possibile eliminare un oggetto [!DNL Catalog] fornendo il relativo ID nel percorso di una richiesta DELETE.

>[!WARNING]
>
>Presta particolare attenzione durante l’eliminazione degli oggetti, poiché questa operazione non può essere annullata e potrebbe causare modifiche di interruzione altrove in [!DNL Experience Platform].

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>L’endpoint `DELETE /batches/{ID}` è stato dichiarato obsoleto. Per eliminare un batch, devi utilizzare l&#39; [API di acquisizione batch](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di oggetto [!DNL Catalog] da eliminare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Identificatore dell&#39;oggetto specifico che si desidera aggiornare. |

**Richiesta**

La seguente richiesta elimina un set di dati il cui ID è specificato nel percorso della richiesta.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>Se nessun oggetto [!DNL Catalog] corrisponde all’ID fornito nella richiesta, è comunque possibile che si riceva un codice di stato HTTP 200, ma l’array di risposta sarà vuoto.
