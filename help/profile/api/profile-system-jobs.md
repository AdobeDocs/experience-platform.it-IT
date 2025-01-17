---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di sistema profilo
type: Documentation
description: Adobe Experience Platform consente di eliminare un set di dati o un batch dall’archivio profili per rimuovere i dati Profilo cliente in tempo reale che non sono più necessari o che sono stati aggiunti per errore. A tal fine è necessario utilizzare l’API di profilo per creare un processo di sistema del profilo o eliminare una richiesta.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 16778d0edbad4539a4ff5084a2f22ca5f08e83ec
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 2%

---

# Endpoint &quot;profile system jobs&quot; (richieste di eliminazione)

>[!IMPORTANT]
>
>I seguenti endpoint possono variare tra le implementazioni di Adobe Experience Platform in esecuzione su Microsoft Azure e Amazon Web Services (AWS). Un Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta l&#39;[panoramica sul cloud multiplo di Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Adobe Experience Platform consente di acquisire dati da più origini e di creare profili affidabili per i singoli clienti. I dati acquisiti in [!DNL Platform] sono memorizzati in [!DNL Data Lake] e se i set di dati sono stati abilitati per il profilo, tali dati vengono memorizzati anche nell&#39;archivio dati [!DNL Real-Time Customer Profile]. Talvolta può essere necessario eliminare i dati di profilo associati a un set di dati dall’archivio Profili per rimuovere i dati non più necessari o che sono stati aggiunti per errore. È necessario utilizzare l&#39;API [!DNL Real-Time Customer Profile] per creare un processo di sistema [!DNL Profile] o &quot;richiesta di eliminazione&quot;.

>[!NOTE]
>
>Se si sta tentando di eliminare set di dati o batch da [!DNL Data Lake], visitare la [panoramica del servizio catalogo](../../catalog/home.md) per ulteriori informazioni.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte di [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, consulta la [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida alla lettura delle chiamate API di esempio in questo documento e per le informazioni importanti sulle intestazioni necessarie per effettuare correttamente le chiamate a qualsiasi API di Experience Platform.

## Visualizzare le richieste di eliminazione {#view}

Una richiesta di eliminazione è un processo asincrono a lungo termine, il che significa che l’organizzazione potrebbe eseguire più richieste di eliminazione contemporaneamente. Per visualizzare tutte le richieste di eliminazione attualmente in esecuzione nell&#39;organizzazione, è possibile eseguire una richiesta GET all&#39;endpoint `/system/jobs`.

Puoi anche utilizzare parametri di query facoltativi per filtrare l’elenco delle richieste di eliminazione restituite nella risposta. Per utilizzare più parametri, separare ogni parametro utilizzando una e commerciale (`&`).

**Formato API**

>[!AVAILABILITY]
>
>I seguenti parametri di query sono disponibili **solo** quando si utilizza Platform in Microsoft Azure.
>
>Quando si utilizza questo endpoint su AWS, i primi 100 processi di sistema vengono restituiti in ordine decrescente, in base alla data di creazione.

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione | Esempio |
| --------- | ----------- | ------- |
| `start` | Offset della pagina dei risultati restituiti, in base all’ora di creazione della richiesta. | `start=4` |
| `limit` | Limita il numero di risultati restituiti. | `limit=10` |
| `page` | Restituisce una pagina di risultati specifica, in base all’ora di creazione della richiesta. | `page=2` |
| `sort` | Ordinare i risultati per un campo specifico in ordine crescente (`asc`) o decrescente (`desc`). Il parametro sort non funziona quando si restituiscono più pagine di risultati. | `sort=batchId:asc` |

**Richiesta**

>[!IMPORTANT]
>
>La richiesta seguente è diversa tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Richiesta di esempio per visualizzare i processi di sistema.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>**è necessario** utilizzare l&#39;intestazione di richiesta `x-sandbox-id` invece dell&#39;intestazione di richiesta `x-sandbox-name` quando si utilizza questo endpoint con AWS.

+++ Richiesta di esempio per visualizzare i processi di sistema.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
```

+++

>[!ENDTABS]

**Risposta**

>[!IMPORTANT]
>
>La seguente risposta differisce tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

In caso di esito positivo, la risposta include un array &quot;figlio&quot; con un oggetto per ogni richiesta di eliminazione contenente i dettagli della richiesta.

+++ Risposta corretta per la visualizzazione delle richieste di eliminazione

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{ORG_ID}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{ORG_ID}",
      "dataSetId": "5c802d3cd83fc114b741c4b5",
      "jobType": "DELETE",
      "status": "PROCESSING",
      "metrics": "{\"recordsProcessed\":0,\"timeTakenInSec\":15}",
      "createEpoch": 1559025404,
      "updateEpoch": 1559025406
    }
  ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `_page.count` | Numero totale di richieste. La risposta è stata troncata per motivi di spazio. |
| `_page.next` | Se esiste una pagina di risultati aggiuntiva, visualizzare la pagina di risultati successiva sostituendo il valore ID in una [richiesta di ricerca](#view-a-specific-delete-request) con il valore `"next"` fornito. |
| `jobType` | Tipo di processo da creare. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. I valori possibili sono `"NEW"`, `"PROCESSING"`, `"COMPLETED"` e `"ERROR"`. |
| `metrics` | Oggetto che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo impiegato per il completamento della richiesta (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

In caso di esito positivo, la risposta restituisce un array contenente un oggetto per ciascuna richiesta di sistema.

+++ Risposta corretta per la visualizzazione delle richieste di sistema

```json
{
    [
        {
            "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
            "requestType": "DELETE_EE_BATCH",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        },
        {
            "requestId": "38a835eb-b491-4864-902b-be07fa4d6a6d",
            "requestType": "TRUNCATE_DATASET",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxName": "prod",
                "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
            },
            "status": "SUCCESS",
            "properties": {
                "datasetId": "66a92c5910df2d1767de13f3"
            },
            "createdAt": "2024-12-22T19:44:50.250006Z",
            "updatedAt": "2024-12-22T19:52:13.380706Z"
        }        
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `requestId` | ID del processo di sistema. |
| `requestType` | Tipo di processo di sistema. I valori possibili sono `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | Stato del processo di sistema. I valori possibili includono `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Oggetto che contiene gli ID di batch e/o set di dati del processo di sistema. |

+++

>[!ENDTABS]

## Creare una richiesta di eliminazione {#create-a-delete-request}

L&#39;avvio di una nuova richiesta di eliminazione viene eseguito tramite una richiesta POST all&#39;endpoint `/systems/jobs`, in cui l&#39;ID del set di dati o del batch da eliminare viene fornito nel corpo della richiesta.

### Eliminare un set di dati e i dati del profilo associati

Per eliminare un set di dati e tutti i dati di profilo associati al set di dati dall’archivio profili, l’ID del set di dati deve essere incluso nel corpo della richiesta POST. Questa azione eliminerà TUTTI i dati per un dato set di dati. [!DNL Experience Platform] consente di eliminare i set di dati basati su schemi di record e serie temporali.

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

>[!IMPORTANT]
>
>La richiesta seguente è diversa tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Richiesta di esempio per eliminare un set di dati.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Proprietà | Descrizione |
| -------- | ----------- |
| `dataSetId` | ID del set di dati da eliminare. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>**è necessario** utilizzare l&#39;intestazione di richiesta `x-sandbox-id` invece dell&#39;intestazione di richiesta `x-sandbox-name` quando si utilizza questo endpoint con AWS.

+++ Richiesta di esempio per eliminare un set di dati.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

+++

| Proprietà | Descrizione |
| -------- | ----------- |
| `dataSetId` | ID del set di dati da eliminare. |

>[!ENDTABS]

**Risposta**

>[!IMPORTANT]
>
>La seguente risposta differisce tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `status` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l&#39;elaborazione. Il `dataSetId` nella risposta deve corrispondere al `dataSetId` inviato nella richiesta.

+++ Risposta corretta per la creazione di una richiesta di eliminazione.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{ORG_ID}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `dataSetId` | ID del set di dati, come specificato nella richiesta POST. |

+++

>[!TAB Amazon Web Services (AWS)]

In caso di esito positivo, la risposta restituisce i dettagli della richiesta di sistema appena creata.

+++ Risposta corretta per la creazione di una richiesta di eliminazione.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `requestId` | ID del processo di sistema. |
| `requestType` | Tipo di processo di sistema. I valori possibili sono `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | Stato del processo di sistema. I valori possibili includono `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Oggetto che contiene gli ID di batch e/o set di dati del processo di sistema. |

+++

>[!ENDTABS]

### Eliminare un batch

Per eliminare un batch, l’ID del batch deve essere incluso nel corpo della richiesta POST. Si noti che non è possibile eliminare batch per set di dati basati su schemi di record. È possibile eliminare solo i batch per i set di dati basati su schemi di serie temporali.

>[!NOTE]
>
> Il motivo per cui non è possibile eliminare i batch per i set di dati basati su schemi di record è che i batch di set di dati di tipo record sovrascrivono i record precedenti e pertanto non possono essere &quot;annullati&quot; o eliminati. L’unico modo per rimuovere l’impatto di batch errati per i set di dati basati su schemi di record consiste nel riacquisire il batch con i dati corretti in modo da sovrascrivere i record errati.

Per ulteriori informazioni sul comportamento di record e serie temporali, consulta la [sezione sui comportamenti dei dati XDM](../../xdm/home.md#data-behaviors) nella panoramica di [!DNL XDM System].

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

>[!IMPORTANT]
>
>La richiesta seguente è diversa tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Richiesta di esempio per eliminare un batch.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Proprietà | Descrizione |
| -------- | ----------- |
| `datasetId` | ID del set di dati per il batch da eliminare. |
| `batchId` | ID del batch da eliminare. |

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>**è necessario** utilizzare l&#39;intestazione di richiesta `x-sandbox-id` invece dell&#39;intestazione di richiesta `x-sandbox-name` quando si utilizza questo endpoint con AWS.

+++ Richiesta di esempio per eliminare un batch.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "datasetId": "66a92c5910df2d1767de13f3",
        "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

+++

| Proprietà | Descrizione |
| -------- | ----------- |
| `datasetId` | ID del set di dati per il batch da eliminare. |
| `batchId` | ID del batch da eliminare. |

>[!ENDTABS]

**Risposta**

>[!IMPORTANT]
>
>La seguente risposta differisce tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `"status"` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l&#39;elaborazione. Il valore `"batchId"` nella risposta deve corrispondere al valore `"batchId"` inviato nella richiesta.

+++ Risposta corretta per la creazione di una richiesta di eliminazione.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "66a92c5910df2d1767de13f3",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `datasetId` | ID del set di dati specificato. |
| `batchId` | ID del batch, come specificato nella richiesta POST. |

+++

>[!TAB Amazon Web Services (AWS)]

In caso di esito positivo, la risposta restituisce i dettagli della richiesta di sistema appena creata.

+++ Risposta corretta per la creazione di una richiesta di eliminazione.

```json
{
    "requestId": "80a9405a-21ca-4278-aedf-99367f90c055",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `requestId` | ID del processo di sistema. |
| `requestType` | Tipo di processo di sistema. I valori possibili sono `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | Stato del processo di sistema. I valori possibili includono `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Oggetto che contiene gli ID di batch e/o set di dati del processo di sistema. |

+++

>[!ENDTABS]

>[!AVAILABILITY]
>
>La funzionalità seguente è **only** disponibile quando si utilizza Platform in Microsoft Azure.

Se si tenta di avviare una richiesta di eliminazione per un batch di set di dati Record, si verifica un errore a 400 livelli, simile al seguente:

```json
{
    "requestId": "bc4eb29f-63a8-4653-9133-71238884bb81",
    "errors": {
        "400": [
            {
                "code": "500",
                "message": "Batch can only be specified for EE type 'a294e36d382649dab2cc6ad64a41b674'"
            }
        ]
    }
}
```

## Visualizzare una richiesta di eliminazione specifica {#view-a-specific-delete-request}

Per visualizzare una richiesta di eliminazione specifica, inclusi dettagli quali lo stato, è possibile eseguire una richiesta di ricerca (GET) all&#39;endpoint `/system/jobs` e includere l&#39;ID della richiesta di eliminazione nel percorso.

**Formato API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DELETE_REQUEST_ID}` | ID della richiesta di eliminazione che desideri visualizzare. |

**Richiesta**

>[!IMPORTANT]
>
>La richiesta seguente è diversa tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

+++ Richiesta di esempio per visualizzare un processo di profilo.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

>[!TAB Amazon Web Services (AWS)]

>[!IMPORTANT]
>
>**è necessario** utilizzare l&#39;intestazione di richiesta `x-sandbox-id` invece dell&#39;intestazione di richiesta `x-sandbox-name` quando si utilizza questo endpoint con AWS.

+++ Richiesta di esempio per visualizzare un processo di profilo.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

+++

>[!ENDTABS]


**Risposta**

>[!IMPORTANT]
>
>La seguente risposta differisce tra le istanze di Azure e AWS.

>[!BEGINTABS]

>[!TAB Microsoft Azure]

La risposta fornisce i dettagli della richiesta di eliminazione, compreso il suo stato aggiornato. L&#39;ID della richiesta di eliminazione nella risposta (il valore `"id"`) deve corrispondere all&#39;ID inviato nel percorso della richiesta.

+++ Risposta corretta per la visualizzazione di una richiesta di eliminazione.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "COMPLETED",
    "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
    "createEpoch": 1559026134,
    "updateEpoch": 1559026137
}
```

| Proprietà | Descrizione |
| ---------- | ----------- |
| `jobType` | Tipo di processo in fase di creazione. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. I valori possibili sono `NEW`, `PROCESSING`, `COMPLETED` e `ERROR`. |
| `metrics` | Matrice che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo impiegato per il completamento della richiesta (`"timeTakenInSec"`). |

+++

>[!TAB Amazon Web Services (AWS)]

In caso di esito positivo, la risposta restituisce i dettagli della richiesta di sistema specificata.

+++ Risposta corretta per la visualizzazione di una richiesta di eliminazione.

```json
{
    "requestId": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "requestType": "DELETE_EE_BATCH",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxName": "prod",
        "sandboxId": "8129954b-fa83-43ba-a995-4bfa8373ba2b"
    },
    "status": "SUCCESS",
    "properties": {
        "batchId": "01JFSYFDFW9JAAEKHX672JMPSB",
        "datasetId": "66a92c5910df2d1767de13f3"
    },
    "createdAt": "2024-12-22T19:44:50.250006Z",
    "updatedAt": "2024-12-22T19:52:13.380706Z"
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `requestId` | ID del processo di sistema. |
| `requestType` | Tipo di processo di sistema. I valori possibili sono `BACKFILL_TTL`, `DELETE_EE_BATCH` e `TRUNCATE_DATASET`. |
| `status` | Stato del processo di sistema. I valori possibili includono `NEW`, `SUCCESS`, `ERROR`, `FAILED` e `IN-PROGRESS`. |
| `properties` | Oggetto che contiene gli ID di batch e/o set di dati del processo di sistema. |

+++

>[!ENDTABS]

Quando lo stato della richiesta di eliminazione è `"COMPLETED"`, è possibile confermare che i dati sono stati eliminati tentando di accedere ai dati eliminati tramite l&#39;API di accesso ai dati. Per istruzioni su come utilizzare l&#39;API di accesso ai dati per accedere ai set di dati e ai batch, consulta la [documentazione sull&#39;accesso ai dati](../../data-access/home.md).

## Rimuovere una richiesta di eliminazione

>[!AVAILABILITY]
>
>Questo endpoint è supportato **only** nell&#39;istanza di Azure di Adobe Experience Platform e **not** nell&#39;istanza di AWS.

[!DNL Experience Platform] consente di eliminare una richiesta precedente, che può essere utile per diversi motivi, tra cui se il processo di eliminazione non è stato completato o si è bloccato nella fase di elaborazione. Per rimuovere una richiesta di eliminazione, è possibile eseguire una richiesta DELETE all&#39;endpoint `/system/jobs` e includere l&#39;ID della richiesta di eliminazione che si desidera rimuovere nel percorso della richiesta.

**Formato API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
| --------- | ----------- |
| {DELETE_REQUEST_ID} | ID della richiesta di eliminazione che desideri rimuovere. |

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare l’eliminazione della richiesta, esegui una richiesta GET per visualizzarla in base al relativo ID. Questo dovrebbe restituire lo stato HTTP 404 (Non trovato), che indica che la richiesta di eliminazione è stata rimossa.

## Passaggi successivi

Ora che si conoscono i passaggi necessari per eliminare i set di dati e i batch da [!DNL Profile store] in [!DNL Experience Platform], è possibile eliminare in modo sicuro i dati aggiunti erroneamente o di cui l&#39;organizzazione non ha più bisogno. Tieni presente che una richiesta di cancellazione non può essere annullata, pertanto devi eliminare solo i dati che ritieni non necessari al momento e che non saranno necessari in futuro.
