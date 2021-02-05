---
keywords: ' Experience Platform;attribuzione ai;punteggi di accesso;argomenti più comuni;download scores;attribuzione dei punteggi;esportazione;esportazione'
solution: Experience Platform, Intelligent Services
title: Scarica i punteggi in  Attribution AI
topic: Downloading scores
description: Questo documento funge da guida per il download dei punteggi per  Attribution AI.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 2%

---


# Scarica i punteggi in  Attribution AI

Questo documento funge da guida per il download dei punteggi per  Attribution AI.

## Introduzione

 Attribution AI consente di scaricare i punteggi nel formato di file Parquet. Questa esercitazione richiede che sia stato letto e completato il download  punteggi delle Attribution AI nella sezione [guida introduttiva](./getting-started.md).

Inoltre, per accedere ai punteggi per  Attribution AI, è necessario disporre di un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visitare la [guida utente  Attribution AI](./user-guide.md). Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

## Trova l&#39;ID del set di dati {#dataset-id}

Nell&#39;istanza del servizio per  informazioni approfondite sulle Attribution AI, fare clic sul menu a discesa *Altre azioni* nella navigazione in alto a destra, quindi selezionare **[!UICONTROL Access scores]**.

![altre azioni](./images/download-scores/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione del punteggio di download e l&#39;ID del set di dati per l&#39;istanza corrente. Copia l’ID del set di dati negli Appunti e passa al passaggio successivo.

![ID set di dati](../customer-ai/images/download-scores/access-scores.png)

## Recupera l&#39;ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, è necessario effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch di successo invece di un elenco di batch appartenenti all’organizzazione. Per restituire altri batch, aumentare il numero del parametro di query `limit` alla quantità desiderata da restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, consultare la guida sul [filtro dei dati del catalogo tramite parametri di query](../../catalog/api/filter-data.md).

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | L&#39;ID del set di dati disponibile nella finestra di dialogo &quot;Access Scores&quot;. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore Key per l&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia l’ID batch da utilizzare nella prossima chiamata API.

>[!NOTE]
>
> Nella risposta seguente è stato riformattato l&#39;oggetto `tags` per garantire la leggibilità.

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
                "id": "5e8f81cf7a4ecb28a8d85b22"
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

## Recuperate la prossima chiamata API con l&#39;ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l&#39;ID batch, potete effettuare una nuova richiesta di GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | L&#39;ID batch recuperato nel passaggio precedente [recupera l&#39;ID batch](#retrieve-your-batch-id). |

**Richiesta**

Utilizzando il proprio ID batch, effettua la seguente richiesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto `_links`. All&#39;interno dell&#39;oggetto `_links` è presente una chiamata `href` con un nuovo valore API. Copiate questo valore per passare al passaggio successivo.

```json
{
    "data": [
        {
            "dataSetFileId": "01E5QSWCAASFQ054FNBKYV6TIQ-1",
            "dataSetViewId": "5e8f81cf7a4ecb28a8d85b22",
            "version": "1.0.0",
            "created": "1586715582571",
            "updated": "1586715582571",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1"
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

Utilizzando il valore `href` ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta di GET per recuperare la directory del file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nel valore `href` dal [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). È accessibile anche nell&#39;array `data` sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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
            "name": "part-00000-tid-5614147572541837832-908bd66a-d856-47fe-b7da-c8e7d22a4097-1370467-1.c000.snappy.parquet",
            "length": "2380211",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet"
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

| Parametro | Descrizione |
| --------- | ----------- |
| `_links.self.href` | L’URL della richiesta di GET utilizzato per scaricare un file nella directory. |


Copiare il valore `href` per qualsiasi oggetto file nell&#39;array `data`, quindi procedere al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, effettuare una richiesta di GET al valore `"href"` copiato nel passaggio precedente [recupero dei file](#retrieving-your-files).

>[!NOTE]
>
>Se effettui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. Nell&#39;esempio di richiesta seguente viene utilizzato `--output {FILENAME.FILETYPE}`.

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
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Prima di effettuare la richiesta, verificate di essere nella directory o nella cartella corretta in cui desiderate salvare il file.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;file.parquet&quot;.

![Terminale](./images/download-scores/terminal-output.png)

I punteggi scaricati saranno in formato Parquet e sarà necessario un [!DNL Spark]-shell o un lettore Parquet per visualizzare i punteggi. Per visualizzare la valutazione non elaborata, potete utilizzare gli [strumenti Apache Parquet](https://github.com/apache/parquet-mr/tree/master/parquet-tools). Gli strumenti Parquet possono analizzare i dati con [!DNL Spark].

## Passaggi successivi

In questo documento sono descritti i passaggi necessari per scaricare  valutazioni delle Attribution AI. Per ulteriori informazioni sulle uscite del punteggio, consultare la [documentazione relativa all&#39;input e all&#39;output dell&#39;AI di attribuzione](./input-output.md).

## Accesso ai punteggi tramite Snowflake

>[!IMPORTANT]
>
>Per ulteriori informazioni sull’accesso ai punteggi tramite Snowflake, contattate attributionai-support@adobe.com.

È possibile accedere ai punteggi aggregati  Attribution AI attraverso il Snowflake. Al momento, è necessario inviare tramite e-mail  supporto del Adobe all&#39;indirizzo attributionai-support@adobe.com per configurare e ricevere le credenziali per l&#39;account del lettore, ad Snowflake.

Una volta che  supporto Adobe ha elaborato la richiesta, vi viene fornito un URL per l&#39;account lettore da Snowflake e le credenziali corrispondenti riportate di seguito:

- URL Snowflake
- Nome utente
- Password

>[!NOTE]
>
>L&#39;account del lettore consente di interrogare i dati utilizzando client SQL, fogli di lavoro e soluzioni BI che supportano il connettore JDBC.

Una volta ottenute le credenziali e l&#39;URL, è possibile eseguire query sulle tabelle dei modelli, aggregate per data punto di contatto o data di conversione.

### Ricerca dello schema nel Snowflake

Utilizzando le credenziali fornite, accedete al Snowflake. Fare clic sulla scheda **Fogli di lavoro** nella navigazione principale in alto a sinistra, quindi passare alla directory del database nel pannello a sinistra.

![Fogli di lavoro e navigazione](./images/download-scores/edited_snowflake_1.png)

Fare clic su **Seleziona schema** nell&#39;angolo superiore destro dello schermo. Nel contenitore visualizzato, verificate di aver selezionato il database corretto. Fare clic sul menu a discesa *Schema* e selezionare uno degli schemi elencati. È possibile eseguire direttamente query dalle tabelle di valutazione elencate nello schema selezionato.

![trovare uno schema](./images/download-scores/edited_snowflake_2.png)

## Collegamento di PowerBI al Snowflake (facoltativo)

Le credenziali di Snowflake possono essere utilizzate per impostare una connessione tra PowerBI Desktop e i database di Snowflake.

Innanzitutto, nella casella *Server* digitare l&#39;URL del Snowflake. Quindi, in *Warehouse* digitare &quot;XSMALL&quot;. Digitare quindi il nome utente e la password.

![esempio di POWERBI](./images/download-scores/powerbi-snowflake.png)

Una volta stabilita la connessione, selezionate il database del Snowflake, quindi selezionate lo schema appropriato. Ora è possibile caricare tutte le tabelle.
