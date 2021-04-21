---
keywords: Experience Platform;download dei punteggi;customer ai;argomenti popolari;esportazione;esportazione;download degli ai clienti;punteggi degli ai clienti
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Scaricare i punteggi in Customer AI
topic-legacy: Downloading scores
description: Customer AI consente di scaricare i punteggi in formato file Parquet.
exl-id: 08f05565-3fd4-4089-9c41-32467f0be751
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 2%

---

# Scaricare i punteggi in Customer AI

Questo documento funge da guida per il download dei punteggi per Customer AI.

## Introduzione

Customer AI consente di scaricare i punteggi in formato file Parquet. Questa esercitazione richiede di aver letto e completato il download dei punteggi di Customer AI nella guida [guida introduttiva](../getting-started.md) .

Inoltre, per accedere ai punteggi per Customer AI, è necessario che sia disponibile un’istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza di servizio, visita [Configurazione di un&#39;istanza di Customer AI](./configure.md). Se hai creato di recente un&#39;istanza di servizio ed è ancora in fase di formazione e valutazione, ti preghiamo di consentire 24 ore per il completamento dell&#39;esecuzione.

Al momento, sono disponibili due modi per scaricare i punteggi di Customer AI:

1. Se desideri scaricare i punteggi a livello individuale e/o non hai abilitato Profilo cliente in tempo reale, passa a [trova l&#39;ID set di dati](#dataset-id).
2. Se il profilo è abilitato e desideri scaricare i segmenti configurati utilizzando Customer AI, passa a [scarica un segmento configurato con Customer AI](#segment).

## Trova l&#39;ID del set di dati {#dataset-id}

Nell’istanza del servizio per informazioni di Customer AI, fai clic sul menu a discesa *Altre azioni* nella navigazione in alto a destra, quindi seleziona **[!UICONTROL Access scores]**.

![altre azioni](../images/insights/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione del download dei punteggi e l’ID del set di dati per l’istanza corrente. Copia l’ID del set di dati negli Appunti e procedi al passaggio successivo.

![ID set di dati](../images/download-scores/access-scores.png)

## Recupera l&#39;ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, devi effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch di successo anziché un elenco di batch appartenenti all’organizzazione. Per restituire batch aggiuntivi, aumenta il numero del parametro della query dei limiti alla quantità desiderata da restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, visita la guida sul [filtraggio dei dati del catalogo utilizzando i parametri di query](../../../catalog/api/filter-data.md).

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | L’ID del set di dati disponibile nella finestra di dialogo &quot;Access Scores&quot; (Punteggi di accesso). |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore chiave per l&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia il tuo ID batch da utilizzare nella prossima chiamata API.

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

## Recupera la prossima chiamata API con il tuo ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l’ID batch, puoi effettuare una nuova richiesta GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID batch recuperato nel passaggio precedente [recupera l&#39;ID batch](#retrieve-your-batch-id). |

**Richiesta**

Utilizzando il tuo ID batch, effettua la seguente richiesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto `_links` . All’interno dell’oggetto `_links` è presente una chiamata `href` con un nuovo valore API. Copia questo valore per passare al passaggio successivo.

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

## Recupera i file {#retrieving-your-files}

Utilizzando il valore `href` ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta GET per recuperare la directory dei file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel valore `href` dal [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). È accessibile anche nella matrice `data` sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta contiene un array di dati che può avere una singola voce o un elenco di file appartenenti a tale directory. L&#39;esempio seguente contiene un elenco di file ed è stato condensato per la leggibilità. In questo scenario, devi seguire l’URL di ciascun file per accedere al file .

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
| `_links.self.href` | L’URL della richiesta di GET utilizzato per scaricare un file nella directory. |


Copiare il valore `href` per qualsiasi oggetto file nell&#39;array `data`, quindi procedere al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, effettua una richiesta di GET al valore `"href"` copiato nel passaggio precedente [recupero dei file](#retrieving-your-files).

>[!NOTE]
>
>Se effettui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. L’esempio di richiesta seguente utilizza `--output {FILENAME.FILETYPE}`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP]
>
>Assicurati di essere nella directory o nella cartella corretta in cui desideri salvare il file prima di effettuare la richiesta GET.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;filename.parquet&quot;.

![Terminale](../images/download-scores/response.png)

## Scaricare un segmento configurato con Customer AI {#segment}

Un modo alternativo per scaricare i dati del punteggio è quello di esportare il pubblico in un set di dati. Dopo che un processo di segmentazione è stato completato correttamente (il valore dell’attributo `status` è &quot;SUCCEEDED&quot;), puoi esportare il pubblico in un set di dati a cui è possibile accedere e agire. Per ulteriori informazioni sulla segmentazione, visita la [panoramica sulla segmentazione](../../../segmentation/home.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo di esportazione, è necessario abilitare Profilo cliente in tempo reale per il set di dati.

La sezione [esportazione di un segmento](../../../segmentation/tutorials/evaluate-a-segment.md) nella guida alla valutazione dei segmenti descrive i passaggi necessari per esportare un set di dati per il pubblico. La guida illustra e fornisce esempi di quanto segue:

- **Creare un set di dati di destinazione:**  crea il set di dati per contenere i membri del pubblico.
- **Genera profili di pubblico nel set di dati:** compila il set di dati con profili singoli XDM in base ai risultati di un lavoro di segmento.
- **Monitora l’avanzamento dell’esportazione:**  controlla l’avanzamento corrente del processo di esportazione.
- **Leggi i dati sul pubblico:** recupera i singoli profili XDM risultanti che rappresentano i membri del pubblico.

## Passaggi successivi

Questo documento descrive i passaggi necessari per scaricare i punteggi di Customer AI. Ora puoi continuare a sfogliare le altre [Intelligent Services](../../home.md) e le guide offerte.
