---
keywords: Experience Platform;attribuzione ai;accedere ai punteggi;argomenti popolari;scaricare i punteggi;attribuzione ai punteggi;esportare;esportare
feature: Attribution AI
title: Scarica punteggi in Attribution AI
description: Questo documento funge da guida per il download dei punteggi per le Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 3%

---

# Scaricare i punteggi nell’Attribution AI

Questo documento funge da guida per il download dei punteggi per le Attribution AI.

## Introduzione

Attribution AI consente di scaricare i punteggi nel formato di file Parquet. Questo tutorial richiede di aver letto e terminato il download della sezione dei punteggi di Attribution AI in [introduzione](./getting-started.md) guida.

Inoltre, per accedere ai punteggi di Attribution AI, è necessario disporre di un’istanza del servizio con uno stato di esecuzione corretto. Per creare una nuova istanza di servizio, visita [Guida utente di Attribution AI](./user-guide.md). Se di recente è stata creata un’istanza del servizio per la quale si sta ancora eseguendo l’apprendimento e il punteggio, attendi 24 ore per il completamento dell’esecuzione.

## Trovare l’ID del set di dati {#dataset-id}

Per Attribution AI approfondimenti nell’istanza di servizio, fai clic su *Altre azioni* nella navigazione in alto a destra, quindi seleziona **[!UICONTROL Punteggi di accesso]**.

![altre azioni](./images/download-scores/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione relativa al download dei punteggi e l’ID del set di dati per l’istanza corrente. Copia l’ID del set di dati negli Appunti e procedi al passaggio successivo.

![ID set di dati](../customer-ai/images/download-scores/access-scores.png)

## Recuperare l’ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, devi effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch riuscito invece di un elenco di batch appartenenti alla tua organizzazione. Per restituire batch aggiuntivi, aumentare il numero di `limit` parametro di query alla quantità desiderata che si desidera restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, consulta la guida su [filtrare i dati del catalogo utilizzando i parametri di query](../../catalog/api/filter-data.md).

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | ID del set di dati disponibile nella finestra di dialogo &quot;Punteggi di accesso&quot;. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore Key dell&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia il tuo ID batch da utilizzare nella chiamata API successiva.

>[!NOTE]
>
> La seguente risposta ha avuto il `tags` oggetto riformato per migliorarne la leggibilità.

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

## Recupera la chiamata API successiva con il tuo ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l’ID batch, potrai effettuare una nuova richiesta GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

**Formato API**

```http
GET batches/{BATCH_ID}/files
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{BATCH_ID}` | ID batch recuperato nel passaggio precedente [recupera il tuo ID batch](#retrieve-your-batch-id). |

**Richiesta**

Utilizzando il tuo ID batch, effettua la seguente richiesta.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un payload contenente `_links` oggetto. All&#39;interno del `_links` l&#39;oggetto è un `href` con una nuova chiamata API come valore. Copia questo valore per passare al passaggio successivo.

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

Utilizzo di `href` valore ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta GET per recuperare la directory dei file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito in `href` valore da [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). È inoltre accessibile nel `data` array sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
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
| `_links.self.href` | URL della richiesta di GET utilizzato per scaricare un file nella directory. |


Copia il `href` valore per qualsiasi oggetto file in `data` , quindi procedere al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, effettua una richiesta GET al `"href"` valore copiato nel passaggio precedente [recupero dei file](#retrieving-your-files).

>[!NOTE]
>
>Se esegui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. L’esempio di richiesta seguente utilizza `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito in `href` valore da un [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). |
| `{FILE_NAME}` | Nome del file. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/01E5QSWCXXYFQ054FNBKYV2BAQ-1?path=part-00000-trd-5714147572541837832-938bd66a-d556-41fe-b7da-c8e7d22a4097-1320467-1.c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'file.parquet'
```

>[!TIP]
>
>Prima di effettuare la richiesta di GET, accertati di trovarti nella directory o nella cartella corretta in cui vuoi salvare il file.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;file.parquet&quot;.

![Terminale](./images/download-scores/terminal-output.png)

I punteggi scaricati saranno in formato Parquet e avranno bisogno di un [!DNL Spark]-shell o lettore Parquet per visualizzare i punteggi. Per la visualizzazione del punteggio non elaborato, puoi utilizzare [Strumenti Apache Parquet](https://parquet.apache.org/docs/). Gli strumenti di Parquet possono analizzare i dati con [!DNL Spark].

## Passaggi successivi

In questo documento sono descritti i passaggi necessari per scaricare i punteggi delle Attribution AI. Per ulteriori informazioni sugli output di punteggio, visitare il sito Web [Input e output di IA per l’attribuzione](./input-output.md) documentazione.

## Accesso ai punteggi con il Snowflake

>[!IMPORTANT]
>
>Per ulteriori informazioni sull’accesso ai punteggi tramite il Snowflake, contatta attributionai-support@adobe.com.

Puoi accedere ai punteggi aggregati delle Attribution AI tramite il Snowflake. Al momento, devi inviare un messaggio e-mail al supporto degli Adobi all’indirizzo attributionai-support@adobe.com per configurare e ricevere le credenziali per il Snowflake per il tuo account di lettore.

Una volta elaborata la richiesta, l’Adobe di supporto ti fornirà l’URL dell’account di lettura da Snowflake e le credenziali corrispondenti:

- URL SNOWFLAKE
- Nome utente
- Password

>[!NOTE]
>
>L&#39;account di lettura consente di eseguire query sui dati utilizzando client SQL, fogli di lavoro e soluzioni BI che supportano il connettore JDBC.

Una volta ottenute le credenziali e l’URL, puoi eseguire una query sulle tabelle modello, aggregate per data di contatto o data di conversione.

### Ricerca dello schema nel Snowflake

Utilizzando le credenziali fornite, accedi al Snowflake. Fai clic su **Fogli di lavoro** nella navigazione principale in alto a sinistra, quindi vai alla directory del database nel pannello a sinistra.

![Fogli di lavoro e navigazione](./images/download-scores/edited_snowflake_1.png)

Quindi, fai clic su **Seleziona schema** nell’angolo in alto a destra dello schermo. Nel popover visualizzato, verificare che sia selezionato il database corretto. Quindi, fai clic su *Schema* e seleziona uno degli schemi elencati. Puoi eseguire query dirette dalle tabelle di punteggio elencate nello schema selezionato.

![trova uno schema](./images/download-scores/edited_snowflake_2.png)

## Collegamento di Power BI al Snowflake (opzionale)

Le credenziali di Snowflake possono essere utilizzate per impostare una connessione tra Power BI Desktop e i database di Snowflake.

In primo luogo, sotto *Server* digitare l&#39;URL del Snowflake. Avanti, sotto *Data warehouse*, digitare &quot;XSMALL&quot;. Quindi, digita il nome utente e la password.

![esempio di POWERBI](./images/download-scores/powerbi-snowflake.png)

Una volta stabilita la connessione, selezionare il database di Snowflake, quindi lo schema appropriato. È ora possibile caricare tutte le tabelle.
