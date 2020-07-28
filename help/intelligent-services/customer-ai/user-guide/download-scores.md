---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: Download dei punteggi nell'AI del cliente
topic: Downloading scores
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---


# Download dei punteggi nell&#39;AI del cliente

Questo documento funge da guida per il download dei punteggi per l&#39;AI del cliente.

## Introduzione

L&#39;AI del cliente consente di scaricare i punteggi nel formato file parquet. Questa esercitazione richiede che sia stata letta e completata la sezione Download dei punteggi AI del cliente nella guida [introduttiva](../getting-started.md) .

Inoltre, per accedere ai punteggi per l&#39;AI cliente, è necessario che sia disponibile un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visita [Configurazione di un&#39;istanza](./configure.md)di AI cliente. Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

Al momento, sono disponibili due modi per scaricare i punteggi AI del cliente:

1. Se desideri scaricare i punteggi a livello individuale e/o non hai abilitato il profilo cliente in tempo reale, inizia con la [ricerca dell&#39;ID](#dataset-id)del set di dati.
2. Se il profilo è abilitato e desideri scaricare i segmenti configurati tramite l&#39;AI del cliente, vai a [scaricare un segmento configurato con l&#39;AI](#segment)del cliente.

## Find your dataset ID {#dataset-id}

Per informazioni approfondite sull&#39;AI del cliente, fai clic sul menu a discesa *Altre azioni* nella barra di navigazione in alto a destra, quindi seleziona **[!UICONTROL Access scores]**.

![altre azioni](../images/insights/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione del punteggio di download e l&#39;ID del set di dati per l&#39;istanza corrente. Copia l’ID del set di dati negli Appunti e passa al passaggio successivo.

![ID set di dati](../images/download-scores/access-scores.png)

## Recupero dell’ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, è necessario effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch di successo invece di un elenco di batch appartenenti all’organizzazione. Per restituire altri batch, aumentare il numero per il parametro della query dei limiti fino alla quantità desiderata che si desidera restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, consulta la guida sul [filtro dei dati del catalogo tramite i parametri](../../../catalog/api/filter-data.md)di query.

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | L&#39;ID del set di dati disponibile nella finestra di dialogo &quot;Access Scores&quot;. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore chiave per l&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia l’ID batch da utilizzare nella prossima chiamata API.

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

## Recuperate la prossima chiamata API con il vostro ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l’ID batch, potete effettuare una nuova richiesta di GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L’ID batch recuperato nel passaggio precedente [recupera l’ID](#retrieve-your-batch-id)batch. |

**Richiesta**

Utilizzando il proprio ID batch, effettua la seguente richiesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un `_links` oggetto. All&#39;interno dell&#39; `_links` oggetto è presente una `href` chiamata API con un nuovo valore. Copiate questo valore per passare al passaggio successivo.

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

Utilizzando il `href` valore ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta di GET per recuperare la directory del file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel `href` valore del passaggio [](#retrieve-the-next-api-call-with-your-batch-id)precedente. È accessibile anche nella `data` matrice sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta contiene un array di dati che può contenere una singola voce o un elenco di file appartenenti a tale directory. L&#39;esempio seguente contiene un elenco di file ed è stato condensato per la leggibilità. In questo scenario, per accedere al file è necessario seguire l&#39;URL di ciascun file.

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


Copiare il `href` valore di qualsiasi oggetto file nell&#39; `data` array, quindi procedere al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, effettuate una richiesta di GET al `"href"` valore copiato nel passaggio precedente [per recuperare i file](#retrieving-your-files).

>[!NOTE]
>
>Se effettui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. Nell&#39;esempio di richiesta seguente viene utilizzato `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel `href` valore di un passaggio [](#retrieve-the-next-api-call-with-your-batch-id)precedente. |
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
>Prima di effettuare la richiesta, verificate di essere nella directory o nella cartella corretta in cui desiderate salvare il file.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;nomefile.parquet&quot;.

![Terminale](../images/download-scores/response.png)

## Download di un segmento configurato con l&#39;API cliente {#segment}

Un metodo alternativo per scaricare i dati della valutazione consiste nell&#39;esportare il pubblico in un dataset. Dopo che un processo di segmentazione è stato completato correttamente (il valore dell&#39; `status` attributo è &quot;SUCCEEDED&quot;), potete esportare il pubblico in un set di dati in cui è possibile accedervi e agire. Per ulteriori informazioni sulla segmentazione, consulta la panoramica [sulla](../../../segmentation/home.md)segmentazione.

>[!IMPORTANT]
>
>Per utilizzare questo metodo di esportazione, è necessario abilitare il profilo cliente in tempo reale per il set di dati.

L’ [esportazione di una sezione di segmento](../../../segmentation/tutorials/evaluate-a-segment.md) nella guida alla valutazione dei segmenti copre i passaggi necessari per esportare un set di dati per l’audience. La guida fornisce alcuni esempi di quanto segue:

- **Crea un set di dati di destinazione:** Create il dataset per contenere i membri del pubblico.
- **Genera profili di audience nel dataset:** Compilare il set di dati con i singoli profili XDM in base ai risultati di un processo di segmento.
- **Monitorare l’avanzamento dell’esportazione:** Verificare l&#39;avanzamento corrente del processo di esportazione.
- **Leggi i dati sul pubblico:** Recuperate i singoli profili XDM risultanti che rappresentano i membri del pubblico.

## Passaggi successivi

Questo documento descrive i passaggi necessari per scaricare i punteggi dell&#39;intelligenza artificiale dei clienti. È ora possibile continuare a consultare gli altri servizi [e guide](../../home.md) intelligenti disponibili.
