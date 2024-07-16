---
keywords: Experience Platform;scaricare punteggi;ia cliente;argomenti popolari;esportare;esportare;download ia cliente;customer ai punteggi
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Scaricare i punteggi in Customer AI
description: IA per l’analisi dei clienti consente di scaricare i punteggi nel formato file Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 3%

---

# Scaricare i punteggi in Customer AI

Questo documento funge da guida per il download dei punteggi per IA per l’analisi dei clienti.

## Introduzione

IA per l’analisi dei clienti consente di scaricare i punteggi nel formato file Parquet. Questo tutorial richiede di aver letto e terminato la sezione download dei punteggi di Customer AI nella [guida introduttiva](../getting-started.md).

Inoltre, per accedere ai punteggi per IA per l’analisi dei clienti, è necessario disporre di un’istanza del servizio con uno stato di esecuzione corretto. Per creare una nuova istanza del servizio, visita [Configurazione di un&#39;istanza di IA per l&#39;analisi dei clienti](./configure.md). Se di recente è stata creata un’istanza del servizio per la quale si sta ancora eseguendo l’apprendimento e il punteggio, attendi 24 ore per il completamento dell’esecuzione.

Attualmente, esistono due modi per scaricare i punteggi di Customer AI:

1. Se desideri scaricare i punteggi a livello individuale e/o non hai Real-Time Customer Profile abilitato, inizia da [trovare il tuo ID set di dati](#dataset-id).
2. Se hai abilitato il profilo e desideri scaricare i segmenti configurati utilizzando IA per l&#39;analisi dei clienti, passa a [scarica un segmento configurato con IA per l&#39;analisi dei clienti](#segment).

## Trovare l’ID del set di dati {#dataset-id}

Nell&#39;istanza del servizio per Customer AI Insights, fai clic sul menu a discesa *Altre azioni* nella navigazione in alto a destra, quindi seleziona **[!UICONTROL Punteggi di accesso]**.

![altre azioni](../images/insights/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione relativa al download dei punteggi e l’ID del set di dati per l’istanza corrente. Copia l’ID del set di dati negli Appunti e procedi al passaggio successivo.

![ID set di dati](../images/download-scores/access-scores.png)

## Recuperare l’ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, devi effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch riuscito invece di un elenco di batch appartenenti alla tua organizzazione. Per restituire batch aggiuntivi, aumenta il numero del parametro di query limit fino alla quantità desiderata da restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, visitare la guida su [filtraggio dei dati del catalogo tramite parametri di query](../../../catalog/api/filter-data.md).

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati disponibile nella finestra di dialogo &quot;Punteggi di accesso&quot;. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore chiave dell&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia il tuo ID batch da utilizzare nella chiamata API successiva.

```json
{
    "01E5QSWCAASFQ054FNBKYV6TIQ": {
        "status": "success",
        "tags": {
            "Tags": [ ... ],
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5cd9146b31dae914b75f654f"
            }
        ],
        "id": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "externalId": "01E5QSWCAASFQ054FNBKYV6TIQ",
        "replay": {
            "predecessors": [
                "01E5N7EDQQP4JHJ93M7C3WM5SP"
            ],
            "reason": "Replacing for 2020-04-09",
            "predecessorListingType": "IMMEDIATE"
        },
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "412657965Y566A4A0A495D4A@AdobeOrg",
        "started": 1586715571808,
        "metrics": {
            "partitionCount": 1,
            "outputByteSize": 2380339,
            "inputFileCount": -1,
            "inputByteSize": 2381007,
            "outputRecordCount": 24340,
            "outputFileCount": 1,
            "inputRecordCount": 24340
        },
        "completed": 1586715582735,
        "created": 1586715571217,
        "createdClient": "acp_foundation_push",
        "createdUser": "sensei_exp_attributionai@AdobeID",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "updated": 1586715583582,
        "version": "1.0.5"
    }
}
```

## Recupera la chiamata API successiva con il tuo ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l&#39;ID batch, puoi effettuare una nuova richiesta GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID batch recuperato nel passaggio precedente [recuperare l&#39;ID batch](#retrieve-your-batch-id). |

**Richiesta**

Utilizzando il tuo ID batch, effettua la seguente richiesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto `_links`. All&#39;interno dell&#39;oggetto `_links` è presente un `href` con una nuova chiamata API come valore. Copia questo valore per passare al passaggio successivo.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

## Recuperare i file {#retrieving-your-files}

Utilizzando il valore `href` ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta GET per recuperare la directory dei file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel valore `href` del [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). È inoltre accessibile nell&#39;array `data` sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta contiene un array di dati che può avere una singola voce o un elenco di file appartenenti a tale directory. L’esempio seguente contiene un elenco di file ed è stato abbreviato per migliorarne la leggibilità. In questo caso, per accedere al file devi seguire l’URL di ciascun file.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `_links.self.href` | URL della richiesta di GET utilizzato per scaricare un file nella directory. |


Copiare il valore `href` per qualsiasi oggetto file nell&#39;array `data`, quindi procedere al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, invia una richiesta GET al valore `"href"` copiato nel passaggio precedente [recupero dei file](#retrieving-your-files).

>[!NOTE]
>
>Se esegui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. Nell&#39;esempio di richiesta seguente viene utilizzato `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel valore `href` da un [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nome del file. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Prima di effettuare la richiesta di GET, accertati di trovarti nella directory o nella cartella corretta in cui vuoi salvare il file.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;filename.parquet&quot;.

![Terminale](../images/download-scores/response.png)

## Scaricare un segmento configurato con Customer AI {#segment}

Un modo alternativo per scaricare i dati di punteggio è esportare il pubblico in un set di dati. Dopo il completamento di un processo di segmentazione (il valore dell&#39;attributo `status` è &quot;RIUSCITO&quot;), è possibile esportare il pubblico in un set di dati in cui è possibile accedervi e agire di conseguenza. Per ulteriori informazioni sulla segmentazione, visita la [panoramica sulla segmentazione](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo di esportazione, è necessario abilitare Real-Time Customer Profile per il set di dati.

La sezione [esportare un segmento](../../../segmentation/tutorials/evaluate-a-segment.md) nella guida alla valutazione dei segmenti descrive i passaggi necessari per esportare un set di dati sul pubblico. La guida illustra e fornisce esempi dei seguenti elementi:

- **Crea un set di dati di destinazione:** Crea il set di dati per contenere i membri del pubblico.
- **Genera profili di pubblico nel set di dati:** Popola il set di dati con profili individuali XDM in base ai risultati di un processo di segmentazione.
- **Monitorare l&#39;avanzamento dell&#39;esportazione:** Controllare l&#39;avanzamento corrente del processo di esportazione.
- **Leggi dati pubblico:** Recupera i profili individuali XDM risultanti che rappresentano i membri del pubblico.

## Passaggi successivi

Questo documento illustra i passaggi necessari per scaricare i punteggi di Customer AI. È ora possibile continuare a sfogliare gli altri [Intelligent Services](../../home.md) e le guide offerte.
