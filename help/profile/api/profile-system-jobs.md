---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Endpoint API per i processi di sistema del profilo
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform consente di eliminare un set di dati o un batch dall’archivio profili per rimuovere i dati del profilo cliente in tempo reale che non sono più necessari o che sono stati aggiunti per errore. Questo richiede l’utilizzo dell’API di profilo per creare un processo del sistema di profili o per eliminare una richiesta.
exl-id: 75ddbf2f-9a54-424d-8569-d6737e9a590e
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 3%

---

# Endpoint dei processi del sistema del profilo (richieste di eliminazione)

Adobe Experience Platform consente di acquisire dati da più sorgenti e di creare profili affidabili per i singoli clienti. I dati acquisiti in [!DNL Platform] vengono memorizzati in [!DNL Data Lake] e, se i set di dati sono stati abilitati per Profilo, tali dati vengono memorizzati anche nell’ [!DNL Real-time Customer Profile] archivio dati. Talvolta può essere necessario eliminare un set di dati o un batch dall’archivio profili per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. È necessario utilizzare l’ API [!DNL Real-time Customer Profile] per creare un processo di sistema [!DNL Profile] o `delete request` che può essere modificato, monitorato o rimosso se necessario.

>[!NOTE]
>
>Se stai tentando di eliminare set di dati o batch da [!DNL Data Lake], visita la [Panoramica del servizio catalogo](../../catalog/home.md) per ulteriori informazioni.

## Introduzione

L&#39;endpoint API utilizzato in questa guida fa parte del [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Prima di continuare, controlla la [guida introduttiva](getting-started.md) per i collegamenti alla relativa documentazione, una guida per la lettura delle chiamate API di esempio in questo documento e informazioni importanti sulle intestazioni necessarie per effettuare chiamate a qualsiasi API di Experience Platform.

## Visualizza richieste di eliminazione

Una richiesta di cancellazione è un processo asincrono di lunga durata, il che significa che l’organizzazione potrebbe eseguire più richieste di eliminazione contemporaneamente. Per visualizzare tutte le richieste di eliminazione attualmente in esecuzione nell’organizzazione, puoi eseguire una richiesta di GET all’endpoint `/system/jobs`.

Puoi inoltre utilizzare parametri di query facoltativi per filtrare l’elenco delle richieste di eliminazione restituite nella risposta. Per utilizzare più parametri, separa ciascun parametro utilizzando una e commerciale (`&`).

**Formato API**

```http
GET /system/jobs
GET /system/jobs?{QUERY_PARAMETERS}
```

| Parametro | Descrizione |
|---|---|
| `start` | Offset la pagina dei risultati restituiti, in base al tempo di creazione della richiesta. Esempio: `start=4` |
| `limit` | Limita il numero di risultati restituiti. Esempio: `limit=10` |
| `page` | Restituisce una pagina specifica di risultati, in base al tempo di creazione della richiesta. Esempio: `page=2` |
| `sort` | Ordinare i risultati in base a un campo specifico in ordine crescente (`asc`) o decrescente (`desc`). Il parametro di ordinamento non funziona quando si restituiscono più pagine di risultati. Esempio: `sort=batchId:asc` |

**Richiesta**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/system/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta include un array &quot;children&quot; con un oggetto per ogni richiesta di eliminazione contenente i dettagli di tale richiesta.

```json
{
  "_page": {
    "count": 100,
    "next": "K1JJRDpFaWc5QUwyZFgtMEpBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQVFBQWZBQUg0Ly9yL25PcmpmZndEZUR3QT0="
  },
  "children": [
    {
      "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
      "imsOrgId": "{IMS_ORG}",
      "batchId": "8d075b5a178e48389126b9289dcfd0ac",
      "jobType": "DELETE",
      "status": "COMPLETED",
      "metrics": "{\"recordsProcessed\":5,\"timeTakenInSec\":1}",
      "createEpoch": 1559026134,
      "updateEpoch": 1559026137
    },
    {
      "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
      "imsOrgId": "{IMS_ORG}",
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
| `_page.count` | Numero totale di richieste. Questa risposta è stata troncata per lo spazio. |
| `_page.next` | Se esiste una pagina aggiuntiva di risultati, visualizza la pagina successiva di risultati sostituendo il valore ID in una [richiesta di ricerca](#view-a-specific-delete-request) con il valore `"next"` fornito. |
| `jobType` | Tipo di processo da creare. In questo caso, restituirà sempre `"DELETE"`. |
| `status` | Lo stato della richiesta di eliminazione. I valori possibili sono `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Un oggetto che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo di completamento della richiesta (`"timeTakenInSec"`). |

## Creare una richiesta di cancellazione {#create-a-delete-request}

L&#39;avvio di una nuova richiesta di eliminazione viene eseguito tramite una richiesta POST all&#39;endpoint `/systems/jobs`, dove l&#39;ID del set di dati o del batch da eliminare viene fornito nel corpo della richiesta.

### Eliminare un set di dati

Per eliminare un set di dati dall’archivio profili, l’ID del set di dati deve essere incluso nel corpo della richiesta di POST. Questa azione eliminerà TUTTI i dati per un dato set di dati. [!DNL Experience Platform] consente di eliminare i set di dati basati sia su schemi di record che su schemi di serie temporali.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "dataSetId": "5c802d3cd83fc114b741c4b5"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `dataSetId` | **(Obbligatorio)** L’ID del set di dati da eliminare. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco generato dal sistema e di sola lettura per la richiesta. Può essere utilizzato per cercare la richiesta e controllarne lo stato. La `status` della richiesta al momento della creazione è `"NEW"` fino a quando non inizia l’elaborazione. La `dataSetId` nella risposta deve corrispondere alla `dataSetId` inviata nella richiesta.

```json
{
    "id": "3f225e7e-ac8c-4904-b1d5-0ce79e03c2ec",
    "imsOrgId": "{IMS_ORG}",
    "dataSetId": "5c802d3cd83fc114b741c4b5",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559025404,
    "updateEpoch": 1559025406
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di cancellazione. |
| `dataSetId` | ID del set di dati, come specificato nella richiesta di POST. |

### Eliminare un batch

Per eliminare un batch, l’ID batch deve essere incluso nel corpo della richiesta POST. Non è possibile eliminare i batch per i set di dati basati su schemi di record. È possibile eliminare solo i batch per i set di dati basati su schemi di serie temporali.

>[!NOTE]
>
> Il motivo per cui non è possibile eliminare i batch per i set di dati basati su schemi di record è perché i batch di set di dati di tipo record sovrascrivono i record precedenti e quindi non possono essere &quot;annullati&quot; o eliminati. L’unico modo per rimuovere l’impatto dei batch errati per i set di dati basati sugli schemi di record è quello di riacquisire il batch con i dati corretti al fine di sovrascrivere i record errati.

Per ulteriori informazioni sul comportamento dei record e delle serie temporali, consulta la sezione sui comportamenti dei dati XDM](../../xdm/home.md#data-behaviors) nella panoramica [!DNL XDM System] .[

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "batchId": "8d075b5a178e48389126b9289dcfd0ac"
      }'
```

| Proprietà | Descrizione |
|---|---|
| `batchId` | **(Obbligatorio)** L&#39;ID del batch da eliminare. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova richiesta di eliminazione creata, incluso un ID univoco generato dal sistema e di sola lettura per la richiesta. Può essere utilizzato per cercare la richiesta e controllarne lo stato. La `"status"` della richiesta al momento della creazione è `"NEW"` fino a quando non inizia l’elaborazione. Il valore `"batchId"` nella risposta deve corrispondere al valore `"batchId"` inviato nella richiesta.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
    "batchId": "8d075b5a178e48389126b9289dcfd0ac",
    "jobType": "DELETE",
    "status": "NEW",
    "createEpoch": 1559026131,
    "updateEpoch": 1559026132
}
```

| Proprietà | Descrizione |
|---|---|
| `id` | ID univoco generato dal sistema e di sola lettura della richiesta di cancellazione. |
| `batchId` | ID del batch, come specificato nella richiesta POST. |

Se tenti di avviare una richiesta di eliminazione per un batch di set di dati di record, incontri un errore a 400 livelli, simile al seguente:

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

## Visualizza una richiesta di cancellazione specifica {#view-a-specific-delete-request}

Per visualizzare una richiesta di cancellazione specifica, inclusi dettagli come il suo stato, puoi eseguire una richiesta di ricerca (GET) all’ endpoint `/system/jobs` e includere l’ID della richiesta di eliminazione nel percorso.

**Formato API**

```http
GET /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| `{DELETE_REQUEST_ID}` | **(Obbligatorio)** L&#39;ID della richiesta di cancellazione che desideri visualizzare. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

La risposta fornisce i dettagli della richiesta di cancellazione, compreso lo stato aggiornato. L’ID della richiesta di cancellazione nella risposta (il valore `"id"`) deve corrispondere all’ID inviato nel percorso della richiesta.

```json
{
    "id": "9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4",
    "imsOrgId": "{IMS_ORG}",
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
| `jobType` | Il tipo di processo da creare, in questo caso restituirà sempre `"DELETE"`. |
| `status` | Lo stato della richiesta di eliminazione. Valori possibili: `"NEW"`, `"PROCESSING"`, `"COMPLETED"`, `"ERROR"`. |
| `metrics` | Matrice che include il numero di record elaborati (`"recordsProcessed"`) e il tempo in secondi di elaborazione della richiesta oppure il tempo di completamento della richiesta (`"timeTakenInSec"`). |

Una volta che lo stato della richiesta di cancellazione è `"COMPLETED"`, puoi confermare che i dati sono stati eliminati tentando di accedere ai dati eliminati utilizzando l’API di accesso ai dati. Per istruzioni su come utilizzare l&#39;API di accesso ai dati per accedere a set di dati e batch, consulta la [documentazione sull&#39;accesso ai dati](../../data-access/home.md).

## Rimuovere una richiesta di cancellazione

[!DNL Experience Platform] consente di eliminare una richiesta precedente, che può essere utile per una serie di motivi, tra cui se il processo di eliminazione non è stato completato o è rimasto bloccato nella fase di elaborazione. Per rimuovere una richiesta di cancellazione, è possibile eseguire una richiesta di DELETE all’ endpoint `/system/jobs` e includere l’ID della richiesta di eliminazione che si desidera rimuovere nel percorso della richiesta.

**Formato API**

```http
DELETE /system/jobs/{DELETE_REQUEST_ID}
```

| Parametro | Descrizione |
|---|---|
| {DELETE_REQUEST_ID} | ID della richiesta di eliminazione che si desidera rimuovere. |

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/system/jobs/9c2018e2-cd04-46a4-b38e-89ef7b1fcdf4 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Risposta**

Una richiesta di eliminazione corretta restituisce lo stato HTTP 200 (OK) e un corpo di risposta vuoto. Puoi confermare che la richiesta è stata eliminata effettuando una richiesta GET per visualizzare la richiesta di cancellazione con il relativo ID. Questo dovrebbe restituire uno stato HTTP 404 (Non trovato), che indica che la richiesta di eliminazione è stata rimossa.

## Passaggi successivi

Ora che conosci i passaggi necessari per eliminare i set di dati e i batch da [!DNL Profile Store] all’interno [!DNL Experience Platform], puoi eliminare in modo sicuro i dati aggiunti in modo errato o di cui la tua organizzazione non ha più bisogno. Ricorda che una richiesta di cancellazione non può essere annullata, pertanto devi solo eliminare i dati di cui sei sicuro che non hai bisogno ora e che non ne avrai bisogno in futuro.
