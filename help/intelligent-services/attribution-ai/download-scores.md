---
keywords: Experience Platform;ai di attribuzione;punteggi di accesso;argomenti popolari;punteggi di download;punteggi di attribuzione;esportazione;esportazione
feature: Attribution AI
title: Scaricare i punteggi in Attribution AI
description: Questo documento funge da guida per il download dei punteggi per Attribution AI.
exl-id: 8821e3fb-c520-4933-8eb7-0b0aa10db916
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 3%

---

# Scaricare i punteggi in Attribution AI

Questo documento funge da guida per il download dei punteggi per Attribution AI.

## Introduzione

Attribution AI consente di scaricare i punteggi in formato file Parquet. Questa esercitazione richiede di aver letto e completato il download della sezione dei punteggi delle Attribution AI nel [guida introduttiva](./getting-started.md) guida.

Inoltre, per accedere ai punteggi per Attribution AI, è necessario che sia disponibile un’istanza di servizio con uno stato di esecuzione riuscito. Per creare una nuova istanza di servizio, visita il [Guida utente di Attribution AI](./user-guide.md). Se hai creato di recente un&#39;istanza di servizio ed è ancora in fase di formazione e valutazione, ti preghiamo di consentire 24 ore per il completamento dell&#39;esecuzione.

## Trova l’ID del set di dati {#dataset-id}

Nell’istanza del servizio per informazioni approfondite sulle Attribution AI, fai clic sul pulsante *Altre azioni* menu a discesa nella navigazione in alto a destra, quindi seleziona **[!UICONTROL Punteggi di accesso]**.

![altre azioni](./images/download-scores/more-actions.png)

Viene visualizzata una nuova finestra di dialogo contenente un collegamento alla documentazione del download dei punteggi e l’ID del set di dati per l’istanza corrente. Copia l’ID del set di dati negli Appunti e procedi al passaggio successivo.

![ID set di dati](../customer-ai/images/download-scores/access-scores.png)

## Recupera l&#39;ID batch {#retrieve-your-batch-id}

Utilizzando l’ID del set di dati del passaggio precedente, devi effettuare una chiamata all’API del catalogo per recuperare un ID batch. Per questa chiamata API vengono utilizzati parametri di query aggiuntivi per restituire l’ultimo batch di successo anziché un elenco di batch appartenenti all’organizzazione. Per restituire batch aggiuntivi, aumenta il numero di `limit` il parametro di query alla quantità desiderata che si desidera restituire. Per ulteriori informazioni sui tipi di parametri di query disponibili, consulta la guida su [filtraggio dei dati del catalogo utilizzando i parametri di query](../../catalog/api/filter-data.md).

**Formato API**

```http
GET /batches?&dataSet={DATASET_ID}&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASET_ID}` | L’ID del set di dati disponibile nella finestra di dialogo &quot;Access Scores&quot; (Punteggi di accesso). |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?&dataSet=5e8f81ce7a4ecb18a8d25b22&createdClient=acp_foundation_push&status=success&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un oggetto ID batch. In questo esempio, il valore Key per l&#39;oggetto restituito è l&#39;ID batch `01E5QSWCAASFQ054FNBKYV6TIQ`. Copia il tuo ID batch da utilizzare nella prossima chiamata API.

>[!NOTE]
>
> La seguente risposta ha avuto `tags` oggetto riformato per la leggibilità.

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

## Recupera la prossima chiamata API con il tuo ID batch {#retrieve-the-next-api-call-with-your-batch-id}

Una volta ottenuto l’ID batch, puoi effettuare una nuova richiesta GET a `/batches`. La richiesta restituisce un collegamento utilizzato come richiesta API successiva.

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
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/01E5QSWCAASFQ054FNBKYV6TIQ/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un payload contenente un `_links` oggetto. All&#39;interno di `_links` un oggetto `href` con una nuova chiamata API come valore. Copia questo valore per passare al passaggio successivo.

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

## Recupera i file {#retrieving-your-files}

Utilizzo della `href` valore ottenuto nel passaggio precedente come chiamata API, effettua una nuova richiesta GET per recuperare la directory file.

**Formato API**

```http
GET files/{DATASETFILE_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nella variabile `href` dal [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). È inoltre accessibile nella `data` matrice sotto il tipo di oggetto `dataSetFileId`. |

**Richiesta**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/01E5QSWCAASFQ054FNBKYV6TIQ-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

La risposta contiene un array di dati che può avere una singola voce o un elenco di file appartenenti a tale directory. L&#39;esempio seguente contiene un elenco di file ed è stato condensato per la leggibilità. In questo scenario, devi seguire l’URL di ciascun file per accedere al file .

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


Copia il `href` per qualsiasi oggetto file nel `data` array, quindi passare al passaggio successivo.

## Scaricare i dati del file

Per scaricare i dati del file, effettua una richiesta di GET al `"href"` valore copiato nel passaggio precedente [recupero dei file](#retrieving-your-files).

>[!NOTE]
>
>Se effettui questa richiesta direttamente nella riga di comando, potrebbe essere richiesto di aggiungere un output dopo le intestazioni della richiesta. Nell&#39;esempio di richiesta seguente viene utilizzato `--output {FILENAME.FILETYPE}`.

**Formato API**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATASETFILE_ID}` | L&#39;ID dataSetFile viene restituito nella variabile `href` da un [passaggio precedente](#retrieve-the-next-api-call-with-your-batch-id). |
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
>Assicurati di essere nella directory o nella cartella corretta in cui desideri salvare il file prima di effettuare la richiesta GET.

**Risposta**

La risposta scarica il file richiesto nella directory corrente. In questo esempio il nome del file è &quot;file.parquet&quot;.

![Terminale](./images/download-scores/terminal-output.png)

I punteggi scaricati saranno in formato Parquet e avranno bisogno di un [!DNL Spark]-shell o lettore di Parquet per visualizzare i punteggi. Per visualizzare il punteggio non elaborato, puoi utilizzare [Strumenti Apache Parquet](https://parquet.apache.org/docs/). Gli strumenti di parquet possono analizzare i dati con [!DNL Spark].

## Passaggi successivi

Questo documento descrive i passaggi necessari per scaricare i punteggi delle Attribution AI. Per ulteriori informazioni sui risultati del punteggio, visita il [Input e output di Attribution AI](./input-output.md) documentazione.

## Accesso ai punteggi utilizzando il Snowflake

>[!IMPORTANT]
>
>Per ulteriori informazioni sull’accesso ai punteggi utilizzando il Snowflake, contatta attributionai-support@adobe.com .

Puoi accedere ai punteggi aggregati delle Attribution AI tramite il Snowflake. Al momento, è necessario inviare un messaggio e-mail al supporto di Adobe all&#39;indirizzo attributionai-support@adobe.com per impostare e ricevere le credenziali al tuo account lettore per Snowflake.

Una volta che il supporto di Adobe ha elaborato la richiesta, ti viene fornito un URL per l’account del lettore al Snowflake e le credenziali corrispondenti di seguito:

- URL Snowflake
- Nome utente
- Password

>[!NOTE]
>
>L&#39;account del lettore consente di eseguire query sui dati utilizzando client sql, fogli di lavoro e soluzioni BI che supportano il connettore JDBC.

Una volta ottenute le credenziali e l’URL, puoi eseguire query sulle tabelle dei modelli, aggregate per data punto di contatto o per data di conversione.

### Ricerca dello schema nel Snowflake

Utilizzando le credenziali fornite, accedi al Snowflake. Fai clic sul pulsante **Fogli di lavoro** scheda nella navigazione principale in alto a sinistra, quindi accedi alla directory del database nel pannello a sinistra.

![Fogli di lavoro e navigazione](./images/download-scores/edited_snowflake_1.png)

Quindi, fai clic su **Seleziona schema** nell’angolo in alto a destra dello schermo. Nel pover visualizzato, verificare di aver selezionato il database corretto. Fai clic su *Schema* e seleziona uno degli schemi elencati. È possibile eseguire query dirette dalle tabelle dei punteggi elencate sotto lo schema selezionato.

![trovare uno schema](./images/download-scores/edited_snowflake_2.png)

## Collegamento di PowerBI al Snowflake (facoltativo)

Le credenziali di Snowflake possono essere utilizzate per impostare una connessione tra i database di PowerBI Desktop e di Snowflake.

Primo, sotto il *Server* digitare l&#39;URL del Snowflake. Successivamente, sotto *Magazzino*, digitare &quot;XSMALL&quot;. Quindi, digita il tuo nome utente e la tua password.

![esempio di POWERBI](./images/download-scores/powerbi-snowflake.png)

Dopo aver stabilito la connessione, seleziona il database di Snowflake, quindi seleziona lo schema appropriato. Ora è possibile caricare tutte le tabelle.
