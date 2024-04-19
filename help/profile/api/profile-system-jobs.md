---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per processi di sistema profilo
type: Documentation
description: Adobe Experience Platform consente di eliminare un set di dati o un batch dall’archivio profili per rimuovere i dati Profilo cliente in tempo reale che non sono più necessari o che sono stati aggiunti per errore. A tal fine è necessario utilizzare l’API di profilo per creare un processo di sistema del profilo o eliminare una richiesta.
role: Developer
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 42c83c7449a14eec5b91f82811bce4234e47cb51
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 3%

---

# Endpoint &quot;profile system jobs&quot; (richieste di eliminazione)

Adobe Experience Platform consente di acquisire dati da più origini e di creare profili affidabili per i singoli clienti. Dati acquisiti in [!DNL Platform] è memorizzato in [!DNL Data Lake], e se i set di dati sono stati abilitati per Profilo, tali dati vengono memorizzati nel [!DNL Real-Time Customer Profile] anche l’archivio dati. Talvolta può essere necessario eliminare i dati di profilo associati a un set di dati dall’archivio Profili per rimuovere i dati non più necessari o che sono stati aggiunti per errore. A tal fine è necessario utilizzare [!DNL Real-Time Customer Profile] API per creare un [!DNL Profile] processo di sistema, oppure `delete request`, che possono anche essere modificate, monitorate o rimosse se necessario.

>[!NOTE]
>
>Se stai tentando di eliminare set di dati o batch da [!DNL Data Lake], visitare il sito [Panoramica di Catalog Service](../../catalog/home.md) per ulteriori informazioni.

## Introduzione

L’endpoint API utilizzato in questa guida fa parte del [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla [guida introduttiva](getting-started.md) per i collegamenti alla documentazione correlata, una guida per la lettura delle chiamate API di esempio di questo documento e informazioni importanti sulle intestazioni richieste necessarie per effettuare correttamente le chiamate a qualsiasi API di Experienci Platform.

## Visualizzare le richieste di eliminazione

Una richiesta di eliminazione è un processo asincrono a lungo termine, il che significa che l’organizzazione potrebbe eseguire più richieste di eliminazione contemporaneamente. Per visualizzare tutte le richieste di eliminazione attualmente in esecuzione nell’organizzazione, è possibile eseguire una richiesta di GET a `/system/jobs` endpoint.

Puoi anche utilizzare parametri di query facoltativi per filtrare l’elenco delle richieste di eliminazione restituite nella risposta. Per utilizzare più parametri, separare ciascun parametro utilizzando una e commerciale (`&`).

**Formato API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `start` | Offset della pagina dei risultati restituiti, in base all’ora di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina di risultati specifica, in base all’ora di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordinare i risultati in base a un campo specifico in modo crescente (`asc`) o decrescente (`desc`). Il parametro sort non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=batchId:asc` |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array &quot;figlio&quot; con un oggetto per ogni richiesta di eliminazione contenente i dettagli della richiesta.

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
|---|---|
| `_page.count` | Numero totale di richieste. La risposta è stata troncata per motivi di spazio. |
| `_page.next` | Se esiste una pagina di risultati aggiuntiva, visualizza la pagina di risultati successiva sostituendo il valore ID in una [richiesta di ricerca](#view-a-specific-delete-request) con `"next"` valore fornito. |
| `jobType` | Tipo di processo da creare. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. I valori possibili sono `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Oggetto che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi in cui la richiesta è stata elaborata o il tempo impiegato per completare la richiesta (`"timeTakenInSec"`). |

## Creare una richiesta di eliminazione {#create-a-delete-request}

L’avvio di una nuova richiesta di eliminazione viene eseguito tramite una richiesta POST a `/systems/jobs` endpoint, in cui l’ID del set di dati o del batch da eliminare viene fornito nel corpo della richiesta.

### Eliminare un set di dati e i dati del profilo associati

Per eliminare un set di dati e tutti i dati di profilo associati al set di dati dall’archivio profili, l’ID del set di dati deve essere incluso nel corpo della richiesta POST. Questa azione eliminerà TUTTI i dati per un dato set di dati. [!DNL Experience Platform] consente di eliminare i set di dati in base a schemi di serie temporali e di record.

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

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

| Proprietà | Descrizione |
|---|---|
| `dataSetId` | **(Obbligatorio)** ID del set di dati da eliminare. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `status` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l’elaborazione. Il `dataSetId` nella risposta deve corrispondere al valore `dataSetId` ha inviato la richiesta.

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
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `dataSetId` | ID del set di dati, come specificato nella richiesta POST. |

### Eliminare un batch

Per eliminare un batch, l’ID del batch deve essere incluso nel corpo della richiesta POST. Si noti che non è possibile eliminare batch per set di dati basati su schemi di record. È possibile eliminare solo i batch per i set di dati basati su schemi di serie temporali.

>[!NOTE]
>
> Il motivo per cui non è possibile eliminare i batch per i set di dati basati su schemi di record è che i batch di set di dati di tipo record sovrascrivono i record precedenti e pertanto non possono essere &quot;annullati&quot; o eliminati. L’unico modo per rimuovere l’impatto di batch errati per i set di dati basati su schemi di record consiste nel riacquisire il batch con i dati corretti in modo da sovrascrivere i record errati.

Per ulteriori informazioni sul comportamento di record e serie temporali, consultare [sezione sui comportamenti dei dati XDM](../../xdm/home.md#data-behaviors) nel [!DNL XDM System] panoramica.

**Formato API**

```http
POST /system/jobs
```

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `batchId` | **(Obbligatorio)** ID del batch da eliminare. |

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco di sola lettura generato dal sistema per la richiesta. Può essere utilizzato per cercare la richiesta e verificarne lo stato. Il `"status"` per la richiesta al momento della creazione è `"NEW"` fino a quando non inizia l’elaborazione. Il `"batchId"` il valore nella risposta deve corrispondere al `"batchId"` valore inviato nella richiesta.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{ORG_ID}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di eliminazione. |
| `batchId` | ID del batch, come specificato nella richiesta POST. |

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

Per visualizzare una richiesta di eliminazione specifica, inclusi dettagli quali lo stato, puoi eseguire una richiesta di ricerca (GET) al `/system/jobs` e includere l’ID della richiesta di eliminazione nel percorso.

**Formato API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obbligatorio)** ID della richiesta di eliminazione che desideri visualizzare. |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta fornisce i dettagli della richiesta di eliminazione, compreso il suo stato aggiornato. L’ID della richiesta di eliminazione nella risposta (il `"id"` deve corrispondere all’ID inviato nel percorso della richiesta.

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
|---|---|
| `jobType` | Il tipo di processo in fase di creazione, in questo caso verrà sempre restituito `"DELETE"`. |
| `status` | Stato della richiesta di eliminazione. Valori possibili: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Matrice che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi in cui la richiesta è stata elaborata o il tempo impiegato per completare la richiesta (`"timeTakenInSec"`). |

Una volta che lo stato della richiesta di eliminazione è `"COMPLETED"` è possibile confermare che i dati sono stati eliminati tentando di accedere ai dati eliminati tramite l’API di accesso ai dati. Per istruzioni su come utilizzare l’API di accesso ai dati per accedere a set di dati e batch, consulta la sezione [Documentazione sull’accesso ai dati](../../data-access/home.md).

## Rimuovere una richiesta di eliminazione

[!DNL Experience Platform] consente di eliminare una richiesta precedente, utile per una serie di motivi, tra cui se il processo di eliminazione non è stato completato o si è bloccato nella fase di elaborazione. Per rimuovere una richiesta di eliminazione, è possibile eseguire una richiesta DELETE al `/system/jobs` e includere nel percorso della richiesta l’ID della richiesta di eliminazione che desideri rimuovere.

**Formato API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| {DELETE_REQUEST_ID} | ID della richiesta di eliminazione che desideri rimuovere. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

In caso di esito positivo, la richiesta di eliminazione restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Per confermare l’eliminazione della richiesta, esegui una richiesta GET per visualizzarla in base al relativo ID. Questo dovrebbe restituire lo stato HTTP 404 (Non trovato), che indica che la richiesta di eliminazione è stata rimossa.

## Passaggi successivi

Ora che conosci i passaggi necessari per eliminare set di dati e batch da [!DNL Profile Store] entro [!DNL Experience Platform], puoi eliminare in modo sicuro i dati che sono stati aggiunti erroneamente o di cui la tua organizzazione non ha più bisogno. Tieni presente che una richiesta di cancellazione non può essere annullata, pertanto devi eliminare solo i dati che ritieni non necessari al momento e che non saranno necessari in futuro.
