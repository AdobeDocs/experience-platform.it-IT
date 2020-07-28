---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Eliminare un oggetto
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---


# Eliminare un oggetto

È possibile eliminare un [!DNL Catalog] oggetto inserendo il relativo ID nel percorso di una richiesta di DELETE.

>[!WARNING]
>
>Prestate particolare attenzione quando eliminate gli oggetti, poiché non è possibile annullarli e potrebbe causare modifiche di interruzione altrove in [!DNL Experience Platform].

**Formato API**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>L&#39; `DELETE /batches/{ID}` endpoint è stato dichiarato obsoleto. Per eliminare un batch, è necessario utilizzare l&#39;API [di](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)inserimento batch.

| Parametro | Descrizione |
| --- | --- |
| `{OBJECT_TYPE}` | Il tipo di [!DNL Catalog] oggetto da eliminare. Gli oggetti validi sono: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Una risposta corretta restituisce lo stato HTTP 200 (OK) e una matrice contenente l&#39;ID del set di dati eliminato. Questo ID deve corrispondere a quello inviato nella richiesta DELETE. L&#39;esecuzione di una richiesta di GET sull&#39;oggetto eliminato restituisce lo stato HTTP 404 (non trovato), a conferma del corretto eliminazione del set di dati.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>Se nessun [!DNL Catalog] oggetto corrisponde all&#39;ID fornito nella richiesta, è comunque possibile che si riceva un codice di stato HTTP 200, ma l&#39;array di risposte sarà vuoto.
