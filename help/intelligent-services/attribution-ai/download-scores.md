---
keywords: Experience Platform;attribution ai;access scores;popular topics
solution: Experience Platform
title: 'Accesso ai punteggi nelle Attribution AI '
topic: Accessing scores
translation-type: tm+mt
source-git-commit: 24449d0138ab449dbc01aecbbe9f70e05c781c89
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 2%

---


# Download dei punteggi in  Attribution AI

Questo documento funge da guida per il download dei punteggi per  Attribution AI.

## Introduzione

 Attribution AI consente di scaricare i punteggi nel formato file parquet. Questa esercitazione richiede che sia stata letta e completata la sezione relativa al download  punteggi delle Attribution AI nella guida [introduttiva](./getting-started.md) .

Inoltre, per accedere ai punteggi per  Attribution AI, è necessario disporre di un&#39;istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza del servizio, visitate la guida [utente](./user-guide.md)Attribution AI. Se avete creato di recente un&#39;istanza di servizio che continua a essere formativa e valutazione, lasciate 24 ore per completare l&#39;esecuzione.

## Find your dataset ID {#dataset-id}

Nell’istanza del servizio per  approfondimenti sulle Attribution AI, fai clic sul menu a discesa *Altre azioni* nella barra di navigazione in alto a destra, quindi seleziona **[!UICONTROL Access scores]**.

![altre azioni](./images/download-scores/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione del punteggio di download e l&#39;ID del set di dati per l&#39;istanza corrente. Copia l’ID del set di dati negli Appunti e passa al passaggio successivo.

![ID set di dati](../customer-ai/images/download-scores/access-scores.png)

## Recupero dell’ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, è necessario effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch di successo invece di un elenco di batch appartenenti all’organizzazione. Per restituire altri batch, aumentare il numero del parametro di `limit` query fino alla quantità desiderata da restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, consulta la guida sul [filtro dei dati del catalogo tramite i parametri](../../catalog/api/filter-data.md)di query.

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
> Nella risposta riportata di seguito l&#39; `tags` oggetto è stato riformattato per la leggibilità.

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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
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

I punteggi scaricati saranno in formato parquet e avrà bisogno di un lettore [!DNL Spark]-shell o parquet per visualizzare i punteggi. Per la visualizzazione della valutazione non elaborata, potete utilizzare gli strumenti [](https://github.com/apache/parquet-mr/tree/master/parquet-tools)parquet. Gli strumenti Parquet consentono di analizzare i dati con [!DNL Spark].

## Passaggi successivi

In questo documento sono descritti i passaggi necessari per scaricare  valutazioni delle Attribution AI. Per maggiori informazioni sulle uscite dei punteggi, consulta la documentazione di input e output [di](./input-output.md) Attribuzione AI.

## Accesso ai punteggi tramite  Snowflake

>[!IMPORTANT]
>
>Per ulteriori informazioni sull&#39;accesso ai punteggi utilizzando  Snowflake, contattate attributionai-support@adobe.com.

È possibile accedere ai punteggi aggregati  Attribution AI tramite  Snowflake. Al momento, è necessario inviare tramite e-mail  supporto del Adobe all&#39;indirizzo attributionai-support@adobe.com per configurare e ricevere le credenziali per  Snowflake nel proprio account lettore.

Una volta che  supporto Adobe ha elaborato la richiesta, vi viene fornito un URL per l&#39;account lettore  Snowflake e le credenziali corrispondenti riportate di seguito:

- URL Snowflake 
- Nome utente
- Password

>[!NOTE]
>
>L&#39;account del lettore consente di interrogare i dati utilizzando client SQL, fogli di lavoro e soluzioni BI che supportano il connettore JDBC.

Una volta ottenute le credenziali e l&#39;URL, è possibile eseguire query sulle tabelle dei modelli, aggregate per data punto di contatto o data di conversione.

### Ricerca dello schema in  Snowflake

Utilizzando le credenziali fornite, accedete al  Snowflake. Fare clic sulla scheda **Fogli** di lavoro nella navigazione principale in alto a sinistra, quindi passare alla directory del database nel pannello a sinistra.

![Fogli di lavoro e navigazione](./images/download-scores/edited_snowflake_1.png)

Fare clic su **Seleziona schema** nell&#39;angolo superiore destro dello schermo. Nel contenitore visualizzato, verificate di aver selezionato il database corretto. Fare clic sul menu a discesa *Schema* e selezionare uno degli schemi elencati. È possibile eseguire direttamente query dalle tabelle di valutazione elencate nello schema selezionato.

![trovare uno schema](./images/download-scores/edited_snowflake_2.png)

## Collegamento di PowerBI al Snowflake  (facoltativo)

Le credenziali  Snowflake possono essere utilizzate per impostare una connessione tra PowerBI Desktop e  database di Snowflake.

Innanzitutto, nella casella *Server* , digitate l’URL  Snowflake. Quindi, in *Warehouse*, digitare &quot;XSMALL&quot;. Digitare quindi il nome utente e la password.

![esempio di POWERBI](./images/download-scores/powerbi-snowflake.png)

Una volta stabilita la connessione, selezionate il database del Snowflake , quindi selezionate lo schema appropriato. Ora è possibile caricare tutte le tabelle.
